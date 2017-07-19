Dropbox
=======

While Dropbox supports the newer OAuth 2.0, Nextcloud uses OAuth 1.0, so
you can safely ignore any references to OAuth 2.0 in the Dropbox
configuration.

Connecting Dropbox is a little more work because you have to create a
Dropbox app. Log into the [Dropbox Developers
page](http://www.dropbox.com/developers) and click **Create Your App**:

![](images/dropbox.png)

Next, for **Choose an API** check **Dropbox API**.

![](images/dropbox-1.png)

The next option is choosing which folders to share, or to share
everything in your Dropbox.

![](images/dropbox-2.png)

Then enter your app name. This is anything you want it to be.

![](images/dropbox-3.png)

Then click the **Create App** button.

Now you are on your app page, which displays its settings and more
options. Do not click **Development (Apply for production)** because
that is for apps that you want to release publicly.

![](images/dropbox-4.png)

Click **Enable additional users** to allow multiple Nextcloud users to
access your new Dropbox share.

Now go to your Nextcloud Admin page. Your Nextcloud configuration
requires only the local mount name, the **App Key** and the **App
Secret**, and which users or groups have access to the share. Remember
the little gear icon at the far right for additional options.

After entering your local mount name, **App Key** and **App Secret**,
click **Grant access**.

![](images/dropbox-6.png)

If you are not already logged into Dropbox, you will be prompted to
login and authorize access. This happens only once, when you are first
creating the new share. Click **Allow**, and you're done.

![](images/dropbox-5.png)

See ../external\_storage\_configuration\_gui for additional mount
options and information.

See auth\_mechanisms for more information on authentication schemes.
