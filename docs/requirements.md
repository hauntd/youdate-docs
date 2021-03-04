# Requirements

To install YouDate script, you need:

- [X] Web-server: Apache 2.4+ or Nginx 1.10+
- [X] PHP[^1]  [<span class="badge badge-danger">7.1 - 7.3</span>](https://www.php.net/supported-versions.php) 
[<span class="badge badge-success">7.4 - 8.0</span>](https://www.php.net/supported-versions.php)
- [X] MySQL <span class="badge badge-success">5.7</span> <span class="badge badge-success">8.0</span>
- [X] PDO PHP extension (enabled by default)
- [X] Mbstring PHP Extension
- [X] Intl PHP Extension
- [X] ICU PHP Extension v49.1+[^2] 
- [X] GD or Imagick PHP Extension
- [X] EXIF extension
- [X] SSL certificate for HTTPS

!!! info "Tip"
    Usually, most of these requirements are already installed on most modern hosting providers, or they are very easy to install on [cloud servers](https://m.do.co/c/fb640e5ae52b).
    
    Not sure if these extensions are installed? Just run the [installer](./installation.md) and it will check automatically
    
!!! info "Tip"
    YouDate will work without SSL certificate, but it's highly recommended using one (besides, OAuth authorization via Facebook/Twitter/etc requires SSL encryption). 
    
    `.htaccess` example for `https`: [config](./https.md)
    
    [Free LetsEncrypt certificate](https://letsencrypt.org/getting-started/) is a good starting point for your web-server.

[^1]: Current YouDate version should work on PHP v7.1, but it's highly recommended upgrading PHP to v7.4 - v8.0. See https://www.php.net/supported-versions.php for more details.
[^2]: 
    Some hosting providers have outdated ICU extension (for example, v4.x was released in [2009](http://site.icu-project.org/download/48)). 
    Modern PHP frameworks such as Yii, Laravel, Symfony require ICU v49+.
