# Installation

You can install YouDate script in two ways: by using web-installer or manually.

## Web-Installer (recommended)

### Requirements check

After uploading files to your web-server/hosting, open your website in the browser. 

!!! note "Website URL"

    In this and the following examples it is `https://youdate.test`.

You will see the initial state of the installation - requirements check page. 

Make sure that everything is ok (all checks pass) and click the "Continue" button.

[![Requirements](./images/requirements.png)](./images/requirements.png)


### Database

The next step is to configure the database.
You must create a database for your script manually (the installer <strong>will not</strong> create it for you).
Then fill out the form and click the "Continue" button.
This action will check the database credentials and import the SQL dump (structure + minimum data).

[![Database](./images/database.png)](./images/database.png)

### Configuration

The next step is to create a config file. This action will verify configuration values, create admin user account and write core config params to the file `.env` file.

[![Config #1](./images/config1.png)](./images/config1.png)
[![Config #2](./images/config2.png)](./images/config2.png)

!!! note "Notes"

    **Admin URL** - administration area URL. If set to **"admin"**, then your administration URL will be like: 
    
    `https://youdate.test/admin`. Please note that `dashboard` prefix is reserved and can't be used.
    
    **Mailer transport** - method to deliver mails. SMTP is recommended (see screenshot). In case when SMTP or Sendmail are failing to deliver e-mails, try `PHP Mail transport`.
    
    **Facebook App ID and Secret** - required for Facebook Login. Visit <a href="https://developers.facebook.com/">developers.facebook.com</a>, follow the manuals, create an app and get the credentials.
    URI for OAuth redirection should be like this:
     
    `https://youdate.test/auth/facebook`

    **Twitter Consumer Key and Secret** - required for Twitter Login. Visit <a href="https://developer.twitter.com/">developer.twitter.com</a>, follow the manuals, create an app and get the credentials.
    URI for OAuth redirection should be like this: 
    
    `https://youdate.test/auth/twitter`

Fill the form, click **Finish** button. Script is almost ready to use. Next step is to configure [cron](./cron.md) commands.

## Manual installation

1. Create a database for YouDate script
2. Import one by one these SQL files:
    * `Files/youdate-manual-installation.sql` 
    * `Files/countries.sql` 
    * `Files/geodata.sql`
3. Open your script directory, find config template `.env-example` and rename it to `.env`
4. Edit `.env` file: set database credentials, define mailer configuration, social auth credentials etc.
5. Make sure that these script directories are writable:
    * `application/runtime`
    * `content/params`
    * `content/images`
    * `content/photos`
    * `content/cache`
6. Default login credentials are:
    * Username: **admin**
    * Password: **adminpassword**
