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

Make sure to create log files for Apache before deployment, the path to apaches log directory may be different depending on factors like your distribution, so make sure to check where it is first.

## More webservers

Currently, no documentation is provided for other web server solutions.

Please refer to the Laravel documentation regarding the setup process for your specific web server solution.
