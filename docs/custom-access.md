In this example profile pages are visible only for logged in users.

See https://www.yiiframework.com/doc/guide/2.0/en/concept-events for more info about Yii2 events.

```php
<?php

namespace mydate\components;

use app\base\Controller;
use app\controllers\ProfileController;
use Yii;
use yii\base\BootstrapInterface;
use yii\base\Event;
use yii\filters\AccessControl;

class ThemeBootstrap extends \youdate\components\ThemeBootstrap implements BootstrapInterface
{
    /**
     * @param \yii\base\Application $app
     */
    public function bootstrap($app)
    {
        parent::bootstrap($app);

        // your customization code goes here
        // ...

        $this->initEvents();
    }

    public function initEvents()
    {
        /*
         * Do not show profiles if user is not logged in
         */
        Event::on(ProfileController::class, ProfileController::EVENT_BEFORE_INIT, function(Event $event) {
            if (Yii::$app->user->isGuest) {
                /** @var Controller $controller */
                $controller = $event->sender;
                $controller->attachBehavior('access', [
                    'class' => AccessControl::class,
                    'rules' => [
                        ['allow' => false],
                    ],
                ]);
            }
        });
    }
}
```
