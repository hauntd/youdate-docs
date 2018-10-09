# Requirements

To install YouDate script, you need:

* Web-server: Apache 2.0 or higher
* PHP 7.0 or higher
* MySQL 5.5 or higher
* PDO PHP extension (enabled by default)
* Mbstring PHP Extension
* Intl PHP Extension
* ICU PHP Extension v49.1+
* GD or Imagick PHP Extension
* EXIF extension
* SSL certificate for HTTPS

!!! info "Tip"
    Usually, most of these requirements are already installed on most modern hosting providers or they are very easy to install on [cloud servers](https://m.do.co/c/fb640e5ae52b).
    
    Not sure if these extensions are installed? Just run the [installer](./installation.md) and it will check automatically
    
!!! info "Tip"
    YouDate will work without SSL certificate, but it's highly recommended to use one (besides, OAuth authorization via Facebook/Twitter/etc requires SSL encryption). 
    
    [Free LetsEncrypt certificate](https://letsencrypt.org/getting-started/) is a good starting point for your web-server.
