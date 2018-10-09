### Hourly/Daily Cron

YouDate requires three CRON commands: two for common tasks (**hourly, daily**) and one for queue processing.

!!! tip "Cron setup on Ubuntu/Debian"

    To setup cron commands on Ubuntu/Debian, read this answer: [https://askubuntu.com/a/2369](https://askubuntu.com/a/2369)

Hourly and daily examples:
   
```sh
30 * * * * /path/to/youdate/application/yii cron/hourly >/dev/null 2>&1
0 18 * * * /path/to/youdate/application/yii cron/daily >/dev/null 2>&1               
```

Some hosting providers are not allowing to use cron commands properly. Instead of this, they allow running cron commands using `wget`.

For this case you can create `cron.php` file (or any other file name) with this content:

```php
<?php

require(__DIR__ . '/application/bootstrap.php');
require(__DIR__ . '/application/vendor/autoload.php');
require(__DIR__ . '/application/environment.php');
require(__DIR__ . '/application/vendor/yiisoft/yii2/Yii.php');

$config = require(__DIR__ . '/application/config/console.php');
$application = new yii\console\Application($config);

$action = isset($_GET['action']) ? $_GET['action'] : null;
$availableCommands = ['cron/hourly', 'cron/daily', 'queue/run'];
if (in_array($action, $availableCommands)) {
    $application->runAction($action);
} else {
    die("$action not supported");
}
```

Your cron commands will look like this: 
```sh
30 * * * * /path/to/usr/bin/wget -O /dev/null https://youdate.local/cron.php?action=cron/hourly
0 18 * * * /path/to/usr/bin/wget -O /dev/null https://youdate.local/cron.php?action=cron/daily
* * * * * /path/to/usr/bin/wget -O /dev/null https://youdate.local/cron.php?action=queue/run
```
                   
### Queue processing

For jobs queue processing (sending mails, notifications etc) you need to run your queue command. You can do this in two ways:

#### Using cron

Add this cron command to run every minute:

```sh
* * * * * /path/to/youdate/application/yii queue/run >/dev/null 2>&1
```

#### Using supervisor system service (*recommended*)
             
It's even better to process queue with Supervisor or Systemd.
 
For more details visit official [yii2-queue module docs](https://github.com/yiisoft/yii2-queue/blob/master/docs/guide/worker.md).
            