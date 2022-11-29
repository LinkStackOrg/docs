# Email verification

With this setting, you can select if you want new users to verify their email address before they’re allowed to use your LittleLink Custom instance.

This setting requires the use of an SMTP Mail server. Luckily, LittleLink Custom includes a free to use SMTP server by default which is already setup for you.

By default, email verification is required for new users, but this can be turned off by changing the key ``REGISTER_AUTH`` from the default value ``verified`` to ``auth``. This skips the verification process, and new users can simply register with any email they want to.

Please note that by disabling email verification, any email could be used to register, the same email would be then used to send ``password reset`` request to. This setting is strongly recommended to be left at the default setting.
