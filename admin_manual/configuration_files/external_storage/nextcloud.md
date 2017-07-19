Nextcloud
=========

An Nextcloud storage is a specialized webdav storage, with optimizations
for Nextcloud-Nextcloud communication. See the webdav documentation to
learn how to configure an Nextcloud external storage.

When filling in the **URL** field, use the path to the root of the
Nextcloud installation, rather than the path to the WebDAV endpoint. So,
for a server at `https://example.com/nextcloud`, use
`https://example.com/nextcloud` and not
`https://example.com/nextcloud/remote.php/dav`.

See ../external\_storage\_configuration\_gui for additional mount
options and information.

See auth\_mechanisms for more information on authentication schemes.
