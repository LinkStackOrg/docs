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

## More webservers

Currently, no documentation is provided for other web server solutions.

Please refer to the Laravel documentation regarding the setup process for your specific web server solution.
