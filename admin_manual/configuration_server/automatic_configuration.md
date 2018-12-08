Automatic Configuration Setup
=============================

If you need to install Nextcloud on multiple servers, you normally do
not want to set up each instance separately as described in
../configuration\_database/linux\_database\_configuration. For this
reason, Nextcloud provides an automatic configuration feature.

To take advantage of this feature, you must create a configuration file,
called ../nextcloud/config/autoconfig.php, and set the file parameters
as required. You can specify any number of parameters in this file. Any
unspecified parameters appear on the "Finish setup" screen when you
first launch Nextcloud.

The ../nextcloud/config/autoconfig.php is automatically removed after
the initial configuration has been applied.

Parameters
----------

When configuring parameters, you must understand that two parameters are
named differently in this configuration file when compared to the
standard config.php file.

  autoconfig.php    config.php
  ----------------- -----------------
  directory         datadirectory
  dbpass            dbpassword

Automatic Configurations Examples
---------------------------------

The following sections provide sample automatic configuration examples
and what information is requested at the end of the configuration.

### Data Directory

Using the following parameter settings, the "Finish setup" screen
requests database and admin credentials settings.

    <?php
    $AUTOCONFIG = array(
      "directory"     => "/www/htdocs/nextcloud/data",
    );

### SQLite Database

Using the following parameter settings, the "Finish setup" screen
requests data directory and admin credentials settings.

    <?php
    $AUTOCONFIG = array(
      "dbtype"        => "sqlite",
      "dbname"        => "nextcloud",
      "dbtableprefix" => "",
    );

### MySQL Database

Using the following parameter settings, the "Finish setup" screen
requests data directory and admin credentials settings.

    <?php
    $AUTOCONFIG = array(
      "dbtype"        => "mysql",
      "dbname"        => "nextcloud",
      "dbuser"        => "username",
      "dbpass"        => "password",
      "dbhost"        => "localhost",
      "dbtableprefix" => "",
    );

> **note**
>
> Keep in mind that the automatic configuration does not eliminate the
> need for creating the database user and database in advance, as
> described in
> ../configuration\_database/linux\_database\_configuration.

### PostgreSQL Database

Using the following parameter settings, the "Finish setup" screen
requests data directory and admin credentials settings.

    <?php
    $AUTOCONFIG = array(
      "dbtype"        => "pgsql",
      "dbname"        => "nextcloud",
      "dbuser"        => "username",
      "dbpass"        => "password",
      "dbhost"        => "localhost",
      "dbtableprefix" => "",
    );

> **note**
>
> Keep in mind that the automatic configuration does not eliminate the
> need for creating the database user and database in advance, as
> described in
> ../configuration\_database/linux\_database\_configuration.

### All Parameters

Using the following parameter settings, because all parameters are
already configured in the file, the Nextcloud installation skips the
"Finish setup" screen.

    <?php
    $AUTOCONFIG = array(
      "dbtype"        => "mysql",
      "dbname"        => "nextcloud",
      "dbuser"        => "username",
      "dbpass"        => "password",
      "dbhost"        => "localhost",
      "dbtableprefix" => "",
      "adminlogin"    => "root",
      "adminpass"     => "root-password",
      "directory"     => "/www/htdocs/nextcloud/data",
    );

> **note**
>
> Keep in mind that the automatic configuration does not eliminate the
> need for creating the database user and database in advance, as
> described in
> ../configuration\_database/linux\_database\_configuration.