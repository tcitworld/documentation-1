Google Drive
============

Nextcloud uses OAuth 2.0 to connect to Google Drive. This requires
configuration through Google to get an app ID and app secret, as
Nextcloud registers itself as an app.

All applications that access a Google API must be registered through the
[Google Cloud Console](https://console.developers.google.com/). Follow
along carefully because the Google interface is a bit of a maze and it's
easy to get lost.

If you already have a Google account, such as Groups, Drive, or Mail,
you can use your existing login to log into the Google Cloud Console.
After logging in click the **Create Project** button.

![](images/google-drive.png)

Give your project a name, and either accept the default **Project ID**
or create your own, then click the **Create** button.

![](images/google-drive1.png)

You'll be returned to your dashboard.

![](images/google-drive2.png)

Google helpfully highlights your next step in blue, the **Use Google
APIs** box. Make sure that your new project is selected, click on **Use
Google APIs** , and it takes you to Google's APIs screen. There are many
Google APIs; look for the **Google Apps APIs** and click **Drive API.**

![](images/google-drive3.png)

**Drive API** takes you to the API Manager overview. Click the blue
**Enable API** button.

![](images/google-drive4.png)

Now you must create your credentials, so click on **Go to credentials**.

![](images/google-drive5.png)

For some reason Google warns us again that we need to create
credentials. We will use 0Auth 2.0.

![](images/google-drive6.png)

Now we have to create a consent screen. This is the information in the
screen Google shows you when you connect your new Google app to
Nextcloud the first time. Click **Configure consent screen**. Then fill
in the required form fields. Your logo must be hosted, as you cannot
upload it, so enter its URL. When you're finished click **Save**.

![](images/google-drive8.png)

The next screen that opens is **Create Client ID**. Check **Web
Application**, then enter your app name. **Authorized JavaScript
Origins** is your root domain, for example `https://example.com`,
without a trailing slash. You need two **Authorized Redirect URIs**, and
they must be in this form:

    https://example.com/nextcloud/index.php/settings/personal/
    https://example.com/nextcloud/index.php/personal/
    https://example.com/nextcloud/index.php/settings/admin/externalstorages
    https://example.com/nextcloud/settings/admin/externalstorages

Replace `https://example.com/nextcloud/` with your own Nextcloud server
URL, then click **Create**.

![](images/google-drive9.png)

Now Google reveals to you your **Client ID** and **Client Secret**.
Click **OK**.

![](images/google-drive10.png)

You can see these anytime in your Google console; just click on your app
name to see complete information.

![](images/google-drive11.png)

Now you have everything you need to mount your Google Drive in
Nextcloud.

Go to the External Storage section of your Admin page, create your new
folder name, enter the Client ID and Client Secret, and click **Grant
Access**. Your consent page appears when Nextcloud makes a successful
connection. Click **Allow**.

![](images/google-drive12.png)

When you see the green light confirming a successful connection you're
finished.

![](images/google-drive13.png)

See ../external\_storage\_configuration\_gui for additional mount
options and information.

See auth\_mechanisms for more information on authentication schemes.
603026686136-qnv9ooocacrkrh1vs0cht83eprgm2sbb.apps.googleusercontent.com
