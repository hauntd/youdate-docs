#### Error An internal server error occurred. The above error occurred while the Web server was processing your request.
  
By default, script does not show error details (they are hidden from users). You can view error details in two ways:

1. Turn on debug in `.env` file: set **`APP_DEBUG = 1`**.

2. Find the log file `application/runtime/logs/app.log`. Your error will be at the end of the file.

3. If there's a script related issue, please send info to [contact@hauntd.me](mailto:contact@hauntd.me)

---

#### The main page is working, 404 error (not found) on any others.

Apache Rewrite module is not enabled or `.htaccess` file is missing.

---

#### Sometimes admin page shows 403 error without any messages

Contact your hosting provider. Most likely you have PHP security extension installed, that may reject requests on some cases. 
*For example:* when you're editing "Additional footer code" and trying to add extra javascript code.

---

#### Script is working, but I cannot see any photos.

It looks like that content directories are not writable. Make sure that these directories are writable:

* `application/runtime` - application logs, cache etc
* `content/assets` - css/js and other generated assets
* `content/photos` - photos
* `content/cache` - cached photos (thumbnails)
* `content/images` - images
* `content/pages` - pages

---

#### Web-camera isn't working in Safari.

Safari requires **https** enabled when accessing web-camera.

---

#### Application error/not working after upgrade.

YouDate couldn't apply updates automatically. You can do this manually by running these commands:
                    
```bash
cd /path/to/youdate/application
php yii migrate/up --interactive=0
php yii cache/flush-all
```
