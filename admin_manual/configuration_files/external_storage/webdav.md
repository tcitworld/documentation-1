WebDAV
======

Use this backend to mount a directory from any WebDAV server, or another
Nextcloud server.

You need the following information:

-   Folder name: The name of your local mountpoint.
-   The URL of the WebDAV or Nextcloud server.
-   Username and password for the remote server
-   Secure <https://>: We always recommend <https://> for security,
    though you can leave this unchecked for <http://>.

Optionally, a `Remote Subfolder` can be specified to change the
destination directory. The default is to use the whole root.

![](images/webdav.png)

> **note**
>
> CPanel users should install [Web
> Disk](https://documentation.cpanel.net/display/ALD/Web+Disk) to enable
> WebDAV functionality.

See ../external\_storage\_configuration\_gui for additional mount
options and information.

See auth\_mechanisms for more information on authentication schemes.
