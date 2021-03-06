Migrating from ownCloud
=======================

> **note**
>
> Especially when migrating from ownCloud to Nextcloud you should
>
> :   create a backup of the config, database and the data directory, in
>     case something goes wrong.
>
Currently migrating from ownCloud is like performing a manual update. So
it is quite easy, to migrate from one ownCloud version to at least one
Nextcloud version. However this does only work with versions that are
close enough database and code-wise. See the table below for a version
map, where migrating is easily possible:

  ownCloud           Nextcloud
  ------------------ ------------------
  10.0.1 or later    12.0.1 or later
  10.0.0             12.0.0
  9.1.x              10.0.x
  9.0.x              10.0.x
  9.0.x              9.0.x

After downloading the correct version of Nextcloud from our [older
releases page](https://nextcloud.com/changelog/), proceed like described
in the manual\_upgrade manual.

Afterwards you can use the Nextcloud updater to update your instance to
the newest version.
