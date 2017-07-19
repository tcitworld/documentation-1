Installation Wizard
===================

Quick Start
-----------

When Nextcloud prerequisites are fulfilled and all Nextcloud files are
installed, the last step to completing the installation is running the
Installation Wizard. This is just three steps:

1.  Point your Web browser to `http://localhost/nextcloud`
2.  Enter your desired administrator's username and password.
3.  Click **Finish Setup**.

![](images/install-wizard-a.png)

You're finished and can start using your new Nextcloud server.

Of course, there is much more that you can do to set up your Nextcloud
server for best performance and security. In the following sections we
will cover important installation and post-installation steps.

-   Data Directory Location &lt;data\_directory\_location\_label&gt;
-   Database Choice &lt;database\_choice\_label&gt;
-   Trusted Domains &lt;trusted\_domains\_label&gt;

Data Directory Location
-----------------------

Click **Storage and Database** to expose additional installation
configuration options for your Nextcloud data directory and database.

![](images/install-wizard-a1.png)

You should locate your Nextcloud data directory outside of your Web root
if you are using an HTTP server other than Apache, or you may wish to
store your Nextcloud data in a different location for other reasons
(e.g. on a storage server). It is best to configure your data directory
location at installation, as it is difficult to move after installation.
You may put it anywhere; in this example is it located in
`/var/oc_data`. This directory must already exist, and must be owned by
your HTTP user.

Database Choice
---------------

SQLite is the default database for Nextcloud Server and it is good only
for testing and lightweight single-user setups without client
synchronization. Supported databases are MySQL, MariaDB, Oracle 11g, and
PostgreSQL, and we recommend MySQL/MariaDB &lt;system\_requirements&gt;.
Your database and PHP connectors must be installed before you run the
Installation Wizard. When you install Nextcloud from packages all the
necessary dependencies will be satisfied (see source\_installation for a
detailed listing of required and optional PHP modules). You will need
the root database login, or any administrator login that has permissions
to create and modify databases, and then enter any name you want for
your Nextcloud database.

After you enter your root or administrator login for your database, the
installer creates a special database user with privileges limited to the
Nextcloud database. Then Nextcloud needs only the special Nextcloud
database user, and drops the root dB login. This user is named for your
Nextcloud admin user, with an `oc_` prefix, and then given a random
password. The Nextcloud database user and password are written into
`config.php`:

    'dbuser' => 'oc_molly',
    'dbpassword' => 'pX65Ty5DrHQkYPE5HRsDvyFHlZZHcm',  

Click Finish Setup, and start using your new Nextcloud server.

![](images/install-wizard-a2.png)

Now we will look at some important post-installation steps.

Trusted Domains
---------------

All URLs used to access your Nextcloud server must be whitelisted in
your `config.php` file, under the `trusted_domains` setting. Users are
allowed to log into Nextcloud only when they point their browsers to a
URL that is listed in the `trusted_domains` setting. You may use IP
addresses and domain names. A typical configuration looks like this:

    'trusted_domains' => 
      array (
       0 => 'localhost', 
       1 => 'server1.example.com', 
       2 => '192.168.1.50',
    ),

The loopback address, `127.0.0.1`, is automatically whitelisted, so as
long as you have access to the physical server you can always log in. In
the event that a load balancer is in place there will be no issues as
long as it sends the correct X-Forwarded-Host header. When a user tries
a URL that is not whitelisted the following error appears:

![](images/install-wizard-a4.png)
