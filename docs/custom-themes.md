YouDate supports two types of themes:

* `full` themes, that include: css, js, images, views (templates) and so on.
* `extended` themes, that have been inherited from `full` themes.

!!! warning "Warning"
    For proper upgrade you should not edit/delete any files in `application` and `content/themes/youdate` directories
    (your changes will be overwritten by new files).
    
!!! info "Info"
    YouDate script comes with `custom` theme which is an extended theme (from `youdate`; demo).

### Starter theme

YouDate comes with extended theme called `mydate` (since v1.4). It's a starting point for theme customization.
Files and directories structure is:

``` sh
.
├─ content/                            # All your content
│  └─ themes/                          # Themes
|     └─ youdate/                      # Default theme
|     └─ custom/                       # Customized theme (example)
|     └─ mydate/                       # Your theme directory (you should edit this one)
|        └─ components/                # Theme components
|           └─ ThemeBootstrap.php      # Theme bootstrap class
|           └─ ThemeSettings.php       # Theme settings class
|        └─ views/                     # Views (templates)
|        └─ theme.json                 # Theme info
|        └─ screenshot.png             # Theme scresnshot (not required)
```

`theme.json` contents:

```json
{
  "title": "MyDate",
  "author": "Alexander Kononenko",
  "website": "https://youdate.hauntd.me/",
  "version": "1.0",
  "namespace": "mydate",
  "extends": "youdate"
}
```

`ThemeBootstrap.php` contents:

```php
<?php

namespace mydate\components;

use yii\base\BootstrapInterface;

/**
 * @author Alexander Kononenko <contact@hauntd.me>
 * @package mydate\components
 */
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
    }
}

```

`ThemeSettings.php` contents:

```php
<?php

namespace mydate\components;

use Yii;

/**
 * @author Alexander Kononenko <contact@hauntd.me>
 * @package mydate\components
 */
class ThemeSettings extends \youdate\components\ThemeSettings
{
    /**
     * @return array
     */
    public function getSettings()
    {
        $settings = [
            // your custom settings
            // see `content/themes/youdate/components/ThemeSettings.php
            // ...
        ];

        return array_merge($settings, parent::getSettings());
    }
}
```

After creating these files and directories you'll be able to switch to your theme. Note, that all theme settings
(`Admin > Themes > Theme settings`) will be empty, because your new theme settings and `youdate` theme settings are stored separately.

### Customizing views (templates)

To customize particular views:

* find them in your parent theme (`content/themes/youdate/views`)
* copy into your new theme (`content/themes/mydate/views`)

**Example**: you want to customize footer, copy `content/themes/youdate/views/partials/footer.php` to 
`content/themes/mydate/views/partials/footer.php`, then edit copied file.
