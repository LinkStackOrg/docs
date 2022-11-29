# Mail Settings

LittleLink Custom comes pre-configured with a free to use built-in SMTP server for sending mail. You can leave this setting as is, if you wish to use this service please read our terms and conditions at [llc-mail.tru.io](http://llc-mail.tru.io).

If you do not wish to use the built-in SMTP server, simply enter your SMTP server credentials in this config section.

- ``MAIL_MAILER``: Either ``smtp`` or ``built-in``. Make sure to change this setting to ``smtp`` if you want to add a custom SMTP server. Default is ``built-in``, if this setting is selected all fields below except ``MAIL_FROM_NAME`` will be ignored.

- ``MAIL_HOST``: SMTP hostname (``smtp.example.com``)

- ``MAIL_PORT``: SMTP port (``465``)

- ``MAIL_USERNAME``: SMTP username

- ``MAIL_PASSWORD``: SMTP password

- ``MAIL_ENCRYPTION``: SMTP encryption method (``TLS``)

- ``MAIL_FROM_ADDRESS``: SMTP sender E-mail address

- ``MAIL_FROM_NAME``: Default is ``${APP_NAME}``. This setting defines the name all mail is sent from. If the default setting is active, the name set in the ``APP_NAME`` section is used to send mail.

