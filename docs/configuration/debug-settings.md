# Debug Settings

Changes if your page should display a full error description instead of a generic error 500 for example.

Settings contain:

- ``APP_DEBUG``: App_debug default is true, but you might want to change this to false after you’re done installing to ensure proper security. This setting is very useful for troubleshooting, but should be turned off in a production environment. If this setting is changed to false, make sure to change the value below as well.

- ``APP_ENV``: App_env, either local or production. Change this to “production” if you set the value above to false.

- ``LOG_CHANNEL``: Can be left at the default value.

- ``LOG_LEVEL``: Can be left at the default value.
