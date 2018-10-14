### Countries list modification.

See https://www.yiiframework.com/doc/guide/2.0/en/concept-events for more info about Yii2 events.

```php
<?php

namespace mydate\components;

use app\helpers\Geographer;
use Yii;
use yii\base\BootstrapInterface;
use yii\base\Event;

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
        Event::on(Geographer::class, Geographer::EVENT_GET_COUNTRIES, function(\app\base\Event $event) {

            /**
             * Remove countries from list
             */
            unset($event->extraData['US']);
            unset($event->extraData['CA']);

            // or

            /**
             * Set only two countries
             */
            $event->extraData = [
                'CA' => Yii::t('app', 'Canada'),
                'US' => Yii::t('app', 'United States'),
            ];
        });
    }
}
```