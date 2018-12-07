### Hourly/Daily Cron and Queue processing

YouDate requires three CRON commands: two for common tasks (**hourly, daily**) and one for queue processing.

!!! tip "Cron setup on Ubuntu/Debian"

    To setup cron commands on Ubuntu/Debian, read this answer: [https://askubuntu.com/a/2369](https://askubuntu.com/a/2369)

Cron commands for hourly/daily tasks and queue processing are:
   
```sh
30 * * * * /path/to/youdate/application/yii cron/hourly >/dev/null 2>&1
0 18 * * * /path/to/youdate/application/yii cron/daily >/dev/null 2>&1               
* * * * * /path/to/youdate/application/yii queue/run --isolate=0 >/dev/null 2>&1               
```

Some hosting providers are not allowing to use cron commands properly. Instead of this, they allow running cron commands using `wget`.

For this case, you can use a file named `cron.php` (see below). Also you should update your `.env` config file: `CRON_SECRET` param must be set.
Example: `CRON_SECRET` is set to *mysecret*, so the cron command will look like this:

```sh
30 * * * * /path/to/usr/bin/wget -O /dev/null https://youdate.local/cron.php?action=cron/hourly&secret=mysecret
0 18 * * * /path/to/usr/bin/wget -O /dev/null https://youdate.local/cron.php?action=cron/daily&secret=mysecret
* * * * * /path/to/usr/bin/wget -O /dev/null https://youdate.local/cron.php?action=queue/run&secret=mysecret
```

```php
<?php

require(__DIR__ . '/application/bootstrap.php');
require(__DIR__ . '/application/vendor/autoload.php');
require(__DIR__ . '/application/environment.php');
require(__DIR__ . '/application/vendor/yiisoft/yii2/Yii.php');

$config = require(__DIR__ . '/application/config/console.php');
$application = new yii\console\Application($config);

// protect with password
if (env('CRON_SECRET') !== false) {
    $secret = $_GET['secret'] ?? null;
    if ($secret !== env('CRON_SECRET')) {
        die("Access denied");
    }
} else {
    die("CRON_SECRET key required (.env file). See https://youdate.hauntd.me/documentation/cron.html for more details");
}

$action = isset($_GET['action']) ? $_GET['action'] : null;
$availableCommands = ['cron/hourly', 'cron/daily', 'queue/run'];

// when pcntl_signal function is not allowed
Yii::$container->set(\yii\queue\db\Command::class, ['isolate' => false]);

if (in_array($action, $availableCommands)) {
    $application->runAction($action);
} else {
    die("$action not supported");
}
```
                   
### Better queue processing (*recommended*)
       
It's better to process queue with Supervisor or Systemd.
 
For more details visit official [yii2-queue module docs](https://github.com/yiisoft/yii2-queue/blob/master/docs/guide/worker.md).

Example config for Supervisor (`/etc/supervisor/conf.d/youdate.conf `):

```ini
[program:youdate-worker]
process_name=%(program_name)s_%(process_num)02d
command=/usr/bin/php /home/youdate/public_html/application/yii queue/listen --verbose=1 --color=0
autostart=true
autorestart=true
user=youdate
numprocs=2
redirect_stderr=true
stdout_logfile=/home/youdate/public_html/application/runtime/queue-worker.log
```
