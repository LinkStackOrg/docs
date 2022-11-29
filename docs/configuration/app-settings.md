# App Settings

App settings change settings regarding your LittleLink Custom installation. You probably only want to change the App Name setting.

These settings include:

- ``APP_NAME``: App_Name changes the displayed name for the App in the title, for example. This can be changed to whatever name you like.

- ``APP_KEY``: One set, you don’t have to change this setting again. Laravel uses the key for all encrypted cookies, including the session cookie, before handing them off to the user’s browser, and it uses it to decrypt cookies read from the browser.

- ``APP_URL``: Default is empty. This field should be left empty under most circumstances. Some Laravel users might be used to populating this section with their public path. This is not required for LittleLink Custom, and you should only change this if required for your setup.
