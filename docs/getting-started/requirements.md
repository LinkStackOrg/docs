# Requirements

**LinkStack under optimal conditions is a simple drag and drop solution with no further configuration required.**

Listed below are all the reqiured modules for LinkStack to run.

## Webserver

- Apache web server/web host with ``.htaccess`` support
- Apache Module ``mod_rewrite``
- At least PHP 8.1 or above
- Read and write access to files in the root directory, as well as files in the directories ``storage`` and ``database``.
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
- XML PHP Extension	

Depending on your database type:

- SQLite PHP Extension (default, no configuration required)
- MySQL PHP Extension


*This documentation only applies to Linkstack instances deployed on a websever. If your instance is deployed as a Docker container, please take a look at the docker specific documentation.*