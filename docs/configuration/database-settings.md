# Database Settings

LittleLink Custom uses a SQLite database by default to ensure an easy setup-process. Since LittleLink Custom is based on Laravel, other database solutions can be used instead, but require further configuration.

``DB_CONNECTION``: Default is SQLite. This setting must not be changed unless you wish to use MySQL instead, please note that this requires further setup.

## Using MySQL

Use the MySQL config from the .env.example config and enter your database credentials.

Run the following commands from your LittleLink Custom installation folder

```
php artisan migrate
php artisan db:seed 
php artisan db:seed --class="AdminSeeder"
php artisan db:seed --class="PageSeeder"
php artisan db:seed --class="ButtonSeeder"
```

For further instructions, please read [this](https://laravel.com/docs/9.x/database).
