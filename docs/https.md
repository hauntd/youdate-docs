By default, the script will work without secure connection (https), except Facebook/Twitter login features. 
Yet it's highly recommended to turn on redirection (http to https). 

`.htaccess` example:

```apacheconfig
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews
    </IfModule>
    RewriteEngine on
    RewriteCond %{HTTPS} !=on
    RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . index.php
</IfModule>

<FilesMatch "\.(gitignore|htaccess|env|env-example)$">
    Order Allow,Deny
    Deny from all
</FilesMatch>

Options All -Indexes
```
