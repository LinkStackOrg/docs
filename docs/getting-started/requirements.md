# Requirements

**Under most conditions, LinkStack is a simple drag and drop solution with no further configuration required.**

While LinkStack is easy to deploy, in order to properly install, it does have basic requirements. The server requirements for where LinkStack will be installed are listed below:

## Webserver

- Apache web server/web host with ``.htaccess`` support
- Apache Module ``mod_rewrite``
- At least PHP 8.1 or above
- Read and write access to files in the root directory, as well as files in the directories ``storage`` and ``database``
- Access over HTTPS/valid SSL certificate

*Other web server types are supported, please refer to [their documentation](./other-webservers.md)*.

## Required PHP modules:

- BCMath PHP Extension
- Ctype PHP Extension
- cURL PHP Extension
- DOM PHP Extension
- Fileinfo PHP Extension
- JSON PHP Extension
- Mbstring PHP Extension
- OpenSSL PHP Extension
- PCRE PHP Extension
- PDO PHP Extension
- Tokenizer PHP Extension
- iconv PHP Extension
- XML PHP Extension

Depending on your database type:

- SQLite PHP Extension (default, no configuration required)
- MySQL PHP Extension

Note: If you are using a **MySQL database** for LinkStack, then you should create the database first. Note the database credentials and the port number MySQL listens on, as you will need this information to complete setup.

*This documentation only applies to the webserver deploy. If you deploy LinkStack as Docker-container, please take a look at the docker specific docs.*
