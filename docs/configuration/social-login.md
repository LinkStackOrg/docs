# Social login

LittleLink Custom social login is provided by Laravel Socialite. You can find the official documentation for this [here](https://laravel.com/docs/9.x/socialite#configuration).

Currently, the social login system supports the following platforms:
`google`, `facebook`, `twitter`

To enable social login and register functionality, first set `ENABLE_SOCIAL_LOGIN` in your config to `true`.

<br>

Next, you will have to get a client ID and client secret for each platform you want to add. To get these values, you will need to use the individual APIs that each platform provides. 
The way to retrieve these credentials differs from provider to provider and will not be documented in this guide.

To get your API access, you will need to enter a redirect URL when retrieving your API credentials.
For your instance, this URL could be `https://example.com/social-auth/provider/callback`.

In the case of Google, this would be: `https://example.com/social-auth/google/callback`.

Make sure to replace example.com with your matching domain name.

<br>

Use the ID and secret for the next step.
You will have to add two new entries to your config per platform you want to add in the format:

- ``PLATFORM_CLIENT_ID``

- ``PLATFORM_CLIENT_SECRET``

- ``PLATFORM_CALLBACK_URL``

For Google, this would be:

- ``GOOGLE_CLIENT_ID=123456789``

- ``GOOGLE_CLIENT_SECRET=abcdef1234567890``

- ``GOOGLE_CALLBACK_URL=https://example.com/social-auth/google/callback``
