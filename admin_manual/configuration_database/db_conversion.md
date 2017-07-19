Converting Database Type
========================

You can convert a SQLite database to a more performing MySQL, MariaDB or
PostgreSQL database with the Nextcloud command line tool. SQLite is good
for testing and simple single-user Nextcloud servers, but it does not
scale for multiple-user production users.

Run the conversion
------------------

First setup the new database, here called "new\_db\_name". In Nextcloud
root folder call

    php occ db:convert-type [options] type username hostname database

The Options

-   `--port="3306"` the database port (optional)
-   `--password="mysql_user_password"` password for the new database. If
    omitted the tool will ask you (optional)
-   `--clear-schema` clear schema (optional)
-   `--all-apps` by default, tables for enabled apps are converted, use
    to convert also tables of deactivated apps (optional)

*Note:* The converter searches for apps in your configured app folders
and uses the schema definitions in the apps to create the new table. So
tables of removed apps will not be converted even with option
`--all-apps`

For example

    php occ db:convert-type --all-apps mysql oc_mysql_user 127.0.0.1 new_db_name

To successfully proceed with the conversion, you must type `yes` when
prompted with the question `Continue with the conversion?`

On success the converter will automatically configure the new database
in your Nextcloud config `config.php`.

Unconvertible Tables
--------------------

If you updated your Nextcloud installation there might exist old tables,
which are not used anymore. The converter will tell you which ones.

:

    The following tables will not be converted:
    oc_permissions
    ...

You can ignore these tables. Here is a list of known old tables:

-   oc\_calendar\_calendars
-   oc\_calendar\_objects
-   oc\_calendar\_share\_calendar
-   oc\_calendar\_share\_event
-   oc\_fscache
-   oc\_log
-   oc\_media\_albums
-   oc\_media\_artists
-   oc\_media\_sessions
-   oc\_media\_songs
-   oc\_media\_users
-   oc\_permissions
-   oc\_queuedtasks
-   oc\_sharing

