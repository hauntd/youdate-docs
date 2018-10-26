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

### Avatar fallback

Gravatar is used by default as an avatar fallback. Since v1.5 you can override this in your theme:

```php
<?php

namespace mydate\components;

use app\base\Event;
use app\events\ProfileEvent;
use app\helpers\Url;
use app\models\Profile;
use yii\base\BootstrapInterface;

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
        // Change avatar fallback from Gravatar to custom png:
        Event::on(Profile::class, Profile::EVENT_AVATAR_FALLBACK, function(ProfileEvent $event) {
            $avatar = null;
            switch ($event->getProfile()->sex) {
                case Profile::SEX_NOT_SET:
                    $avatar = '@extendedThemeUrl/static/images/sex-neutral.png';
                    break;
                case Profile::SEX_MALE:
                    $avatar = '@extendedThemeUrl/static/images/sex-male.png';
                    break;
                case Profile::SEX_FEMALE:
                    $avatar = '@extendedThemeUrl/static/images/sex-female.png';
                    // or
                    $avatar = '@content/avatar.png';
                    // or
                    $avatar = 'https://example.com/some-avatar.png';
                    break;
            }
            $event->getProfile()->fallbackAvatar = Url::to($avatar);
        });
    }
}
```
