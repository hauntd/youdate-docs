**Error An internal server error occurred. The above error occurred while the Web server was processing your request.**
  
By default script does not show error details (they are hidden from users). You can view error details in two ways:

1. Turn on debug in `.env` file: set **`APP_DEBUG = 1`**.

2. Find the log file `application/runtime/logs/app.log`. Your error will be at the end of the file. Also you can create a [ticket](https://youdate.hauntd.me/forum/t/general) and attach that file.

---

**Main page is working, 404 error (not found) on any others.**

Apache Rewrite module is not enabled or `.htaccess` file is missing.

---

**Script is working but I can not see any photos.**

It looks like that content directories are not writable. Make sure that these directories are writable:

* `application/runtime` - application logs, cache etc
* `content/assets` - css/js and other generated assets
* `content/photos` - photos
* `content/cache` - cached photos (thumbnails)
* `content/images` - images
* `content/pages` - pages

---

**Web-camera isn't working in Safari.**

Safari requires **https** enabled when accessing web-camera.

---

**Application error/not working after upgrade.**

YouDate couldn't apply updates automatically. You can do this manually by running these commands:
                    
```bash
cd /path/to/youdate/application
php yii migrate/up --interactive=0
php yii cache/flush-all
```
