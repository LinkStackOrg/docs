# Other webservers

## NGINX

**This is just an example, we assume that you have prior experience setting up NGINX Vhosts!**

<br>

[For further instructions, please refer to the official NGINX documentation provided by Laravel.](https://laravel.com/docs/9.x/deployment#nginx)

<br>

**To ensure proper security, access to certain configuration files must be prevented.**

Example configuration:

```
server {
    listen 80;
    listen [::]:80;
    server_name example.com;
    root /path/to/example.com;
 
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";
 
    index index.php;
 
    charset utf-8;
 
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
 
    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }
 
    error_page 404 /index.php;
 
    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
 
    location ~ /\.(?!well-known).* {
        deny all;
    }
    

location ~ ^\. {
deny all;
}

location ~ \.sqlite$ {
deny all;
}

location ~ \.env$ {
deny all;
}

location ~ /\.htaccess {
allow all;
}
    
}
```

## Apache2

**This is just an example, we assume that you have prior experience setting up Apache Vhosts!**

**Access to configuration files is already denied via `.htaccess` files in the LinkStack root directory.**

<br>

```xml
<VirtualHost *:80>
        ServerName example.com
        ServerAlias www.example.com
        ServerAdmin webmaster@localhost
        DocumentRoot /path/to/example.com
        DirectoryIndex index.htm index.html index.php
        ErrorLog /var/log/httpd/linkstack/error.log
        CustomLog /var/log/httpd/linkstack/access.log combined

        <Directory />
        Options FollowSymLinks
        AllowOverride None
        </Directory>

        <Directory /path/to/example.com/>
        Options -Indexes +MultiViews +FollowSymLinks +ExecCGI
        Require all granted
        AllowOverride all
        </Directory>
</VirtualHost>
```
## Litespeed

**This is just an .htaccess example, we assume that you have prior experience setting up Litespeed - Cyberpanel!** 

```
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews
    </IfModule>

    RewriteEngine On

    # Redirect Trailing Slashes If Not A Folder...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)/$ /$1 [L,R=301]

    # Handle Front Controller...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]

    # Handle Authorization Header
    RewriteCond %{HTTP:Authorization} .
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
</IfModule>

# Restrict access to critical files
<FilesMatch "^\.">
Order allow,deny
Deny from all
</FilesMatch>
<Files ~ "\.sqlite$">
    Order allow,deny
    Deny from all
</Files>
<Files ~ "\.zip$">
    Order allow,deny
    Deny from all
</Files>
```
 
## More webservers

Currently, no documentation is provided for other web server solutions.

Please refer to the Laravel documentation regarding the setup process for your specific web server solution.
