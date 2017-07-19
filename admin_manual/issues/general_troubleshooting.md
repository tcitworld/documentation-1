General Troubleshooting
=======================

If you have trouble installing, configuring or maintaining Nextcloud,
please refer to our community support channels:

-   

    [The Nextcloud Forums](https://help.nextcloud.com)

    :   The Nextcloud forums have a [FAQ
        page](https://help.nextcloud.com/c/faq) where each topic
        corresponds to typical mistakes or frequently occurring issues

-   [The Nextcloud forums](https://help.nextcloud.com)
-   The Nextcloud IRC chat channel `irc://#nextcloud@freenode.net` on
    freenode.net, also accessible via
    [webchat](http://webchat.freenode.net/?channels=nextcloudhttps://docs.nextcloud.org/server/12/developer_manual/bugtracker/index.html)

Please understand that all these channels essentially consist of users
like you helping each other out. Consider helping others out where you
can, to contribute back for the help you get. This is the only way to
keep a community like Nextcloud healthy and sustainable!

If you are using Nextcloud in a business or otherwise large scale
deployment, note that Nextcloud GmbH offers commercial support options.

Bugs
----

If you think you have found a bug in Nextcloud, please:

-   Search for a solution (see the options above)
-   Double-check your configuration

If you can't find a solution, please use our
[bugtracker](https://github.com/nextcloud/server/issues). You can
generate a configuration report with the occ config command 
&lt;config\_commands\_label&gt;, with passwords automatically obscured.

General Troubleshooting
-----------------------

Check the Nextcloud ../installation/system\_requirements, especially
supported browser versions.

When you see warnings about `code integrity`, refer to code\_signing.

### Disable 3rdparty / non-shipped apps

It might be possible that 3rd party / non-shipped apps are causing
various different issues. Always disable 3rd party apps before upgrades,
and for troubleshooting. Please refer to the apps\_commands\_label on
how to disable an app from command line.

### Nextcloud Logfiles

In a standard Nextcloud installation the log level is set to `Normal`.
To find any issues you need to raise the log level to `All` in your
`config.php` file, or to **Everything** on your Nextcloud Admin page.
Please see ../configuration\_server/logging\_configuration for more
information on these log levels.

Some logging - for example JavaScript console logging - needs debugging
enabled. Edit config/config.php and change `'debug' => false,` to
`'debug' => true,` Be sure to change it back when you are finished.

For JavaScript issues you will also need to view the javascript console.
All major browsers have developer tools for viewing the console, and you
usually access them by pressing F12. For Firefox we recommend to
installing the [Firebug extension](https://getfirebug.com/).

> **note**
>
> The logfile of Nextcloud is located in the data directory
> `nextcloud/data/nextcloud.log`.

### PHP Version and Information

You will need to know your PHP version and configurations. To do this,
create a plain-text file named **phpinfo.php** and place it in your Web
root, for example `/var/www/html/phpinfo.php`. (Your Web root may be in
a different location; your Linux distribution documentation will tell
you where.) This file contains just this line:

    <?php phpinfo(); ?>

Open this file in a Web browser by pointing your browser to
`localhost/phpinfo.php`:

![](../images/phpinfo.png)

Your PHP version is at the top, and the rest of the page contains
abundant system information such as active modules, active `.ini` files,
and much more. When you are finished reviewing your information you must
delete `phpinfo.php`, or move it outside of your Web directory, because
it is a security risk to expose such sensitive data.

### Debugging Sync Issues

> **warning**
>
> The data directory on the server is exclusive to Nextcloud and must
> not be modified manually.

Disregarding this can lead to unwanted behaviours like:

-   Problems with sync clients
-   Undetected changes due to caching in the database

If you need to directly upload files from the same server please use a
WebDAV command line client like `cadaver` to upload files to the WebDAV
interface at:

`https://example.com/nextcloud/remote.php/dav`

### Common problems / error messages

Some common problems / error messages found in your logfiles as
described above:

-   `SQLSTATE[HY000] [1040] Too many connections` -&gt; You need to
    increase the connection limit of your database, please refer to the
    manual of your database for more information.
-   `SQLSTATE[HY000]: General error: 5 database is locked` -&gt; You're
    using `SQLite` which can't handle a lot of parallel requests. Please
    consider converting to another database like described
    in ../configuration\_database/db\_conversion.
-   `SQLSTATE[HY000]: General error: 2006 MySQL server has gone away`
    -&gt; Please refer to db-troubleshooting-label for more information.
-   `SQLSTATE[HY000] [2002] No such file or directory` -&gt; There is a
    problem accessing your SQLite database file in your data directory
    (`data/nextcloud.db`). Please check the permissions of this
    folder/file or if it exists at all. If you're using MySQL please
    start your database.
-   `Connection closed / Operation cancelled` -&gt; This could be caused
    by wrong `KeepAlive` settings within your Apache config. Make sure
    that `KeepAlive` is set to `On` and also try to raise the limits of
    `KeepAliveTimeout` and `MaxKeepAliveRequests`.
-   `No basic authentication headers were found` -&gt; This error is
    shown in your `data/nextcloud.log` file. Some Apache modules like
    `mod_fastcgi`, `mod_fcgid` or `mod_proxy_fcgi` are not passing the
    needed authentication headers to PHP and so the login to Nextcloud
    via WebDAV, CalDAV and CardDAV clients is failing. Information on
    how to correctly configure your environment can be found at the
    [forums](https://forum.owncloud.org/viewtopic.php?f=17&t=30646).

Troubleshooting Web server and PHP problems
-------------------------------------------

### Logfiles

When having issues the first step is to check the logfiles provided by
PHP, the Web server and Nextcloud itself.

> **note**
>
> In the following the paths to the logfiles of a default Debian
> installation running Apache2 with mod\_php is assumed. On other Web
> servers, Linux distros or operating systems they can differ.

-   The logfile of Apache2 is located in `/var/log/apache2/error.log`.
-   The logfile of PHP can be configured in your
    `/etc/php5/apache2/php.ini`. You need to set the directive
    `log_errors` to `On` and choose the path to store the logfile in the
    `error_log` directive. After those changes you need to restart your
    Web server.
-   The logfile of Nextcloud is located in the data directory
    `/var/www/nextcloud/data/nextcloud.log`.

### Web server and PHP modules

> **note**
>
> Lighttpd is not supported with Nextcloud, and some Nextcloud features
> may not work at all on Lighttpd.

There are some Web server or PHP modules which are known to cause
various problems like broken up-/downloads. The following shows a draft
overview of these modules:

1.  Apache

-   mod\_pagespeed
-   mod\_evasive
-   mod\_security
-   mod\_reqtimeout
-   mod\_deflate
-   libapache2-mod-php5filter (use libapache2-mod-php5 instead)
-   mod\_spdy together with libapache2-mod-php5 / mod\_php (use fcgi or
    php-fpm instead)
-   mod\_dav
-   mod\_xsendfile / X-Sendfile (causing broken downloads if not
    configured correctly)

2.  NginX

-   ngx\_pagespeed
-   HttpDavModule
-   X-Sendfile (causing broken downloads if not configured correctly)

3.  PHP

-   eAccelerator

Troubleshooting WebDAV
----------------------

Nextcloud uses SabreDAV, and the SabreDAV documentation is comprehensive
and helpful.

See:

-   [SabreDAV FAQ](http://sabre.io/dav/faq/)
-   [Web servers](http://sabre.io/dav/webservers) (Lists lighttpd as
    not recommended)
-   [Working with large files](http://sabre.io/dav/large-files/) (Shows
    a PHP bug in older SabreDAV versions and information for
    mod\_security problems)
-   [0 byte files](http://sabre.io/dav/0bytes) (Reasons for empty files
    on the server)
-   [Clients](http://sabre.io/dav/clients/) (A comprehensive list of
    WebDAV clients, and possible problems with each one)
-   [Finder, OS X's built-in WebDAV
    client](http://sabre.io/dav/clients/finder/) (Describes problems
    with Finder on various Web servers)

There is also a well maintained FAQ thread available at the [ownCloud
Forums](https://forum.owncloud.org/viewtopic.php?f=17&t=7536) which
contains various additional information about WebDAV problems.

Troubleshooting Contacts & Calendar
-----------------------------------

### Service discovery

Some clients - especially on iOS/Mac OS X - have problems finding the
proper sync URL, even when explicitly configured to use it.

If you want to use CalDAV or CardDAV clients together with Nextcloud it
is important to have a correct working setup of the following URLs:

`https://example.com/.well-known/carddav`\
`https://example.com/.well-known/caldav`

Those need to be redirecting your clients to the correct DAV endpoints.
If running Nextcloud at the document root of your Web server the correct
URL is:

`https://example.com/remote.php/dav`

and if running in a subfolder like `nextcloud`:

`https://example.com/nextcloud/remote.php/dav`

For the first case the .htaccess file shipped with Nextcloud should do
this work for your when running Apache. You only need to make sure that
your Web server is using this file. When running Nginx please refer to
../installation/nginx.


If your Nextcloud instance is installed in a subfolder called nextcloud\`
and you're running Apache create or edit the .htaccess file within the
document root of your Web server and add the following lines:

    Redirect 301 /.well-known/carddav /nextcloud/remote.php/dav
    Redirect 301 /.well-known/caldav /nextcloud/remote.php/dav

Now change the URL in the client settings to just use:

`https://example.com`

instead of e.g.

`https://example.com/nextcloud/remote.php/dav/principals/username`.

There are also several techniques to remedy this, which are described
extensively at the [Sabre DAV
website](http://sabre.io/dav/service-discovery/).

### Unable to update Contacts or Events

If you get an error like:

`PATCH https://example.com/remote.php/dav HTTP/1.0 501 Not Implemented`

it is likely caused by one of the following reasons:

Using Pound reverse-proxy/load balancer

:   As of writing this Pound doesn't support the HTTP/1.1 verb. Pound is
    easily
    [patched](http://www.apsis.ch/pound/pound_list/archive/2013/2013-08/1377264673000)
    to support HTTP/1.1.

Misconfigured Web server

:   Your Web server is misconfigured and blocks the needed DAV methods.
    Please refer to trouble-webdav-label above for
    troubleshooting steps.

Other issues
------------

Some services like *Cloudflare* can cause issues by minimizing
JavaScript and loading it only when needed. When having issues like a
not working login button or creating new users make sure to disable such
services first.
