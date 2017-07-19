WebDAV Client API's
===================

This document provides a quick overview of the WebDAV operations
supported in Nextcloud, to keep things readable it won't go into many
details for each operation, further information for each operation can
be found in the corresponding rfc where applicable

----WebDAV Basics ----

The base url for all WebDAV operations for a Nextcloud instance is
`/remote.php/dav`{.sourceCode}.

All requests need to provide authentication information, either as a
Basic Auth header or by passing a set of valid session cookies.

----Testing requests with curl ----

All WebDAV requests can be easily tested out using `curl`{.sourceCode}
by specifying the request method (`GET`{.sourceCode},
`PROPFIND`{.sourceCode}, `PUT`{.sourceCode}, etc) and setting a request
body where needed.

For example: you can perform a `PROPFIND`{.sourceCode} request to find
files in a folder using

``` {.sourceCode .bash}
curl -u username:password 'https://cloud.example.com/remote.php/dav/files/username/folder' -X PROPFIND --data '<?xml version="1.0" encoding="UTF-8"?>
 <d:propfind xmlns:d="DAV:">
   <d:prop xmlns:oc="http://owncloud.org/ns">
     <d:getlastmodified/>
     <d:getcontentlength/>
     <d:getcontenttype/>
     <oc:permissions/>
     <d:resourcetype/>
     <d:getetag/>
   </d:prop>
 </d:propfind>'
```

----Listing Folders ([rfc4918](https://tools.ietf.org/html/rfc4918))
----

The contents of a folder can be listed by sending a
`PROPFIND`{.sourceCode} request to the folder.

``` {.sourceCode .}
PROPFIND remote.php/dav/files/user/path/to/folder
```

\~\~\~\~ Requesting properties \~\~\~\~

By default, a `PROPFIND`{.sourceCode} request will only return a small
number of properties for each file: last modified date, file size,
whether it's a folder, etag and mime type.

You can request additional properties by sending a request body with the
`PROPFIND`{.sourceCode} request that lists all requested properties.

``` {.sourceCode .xml}
<?xml version="1.0"?>
<d:propfind  xmlns:d="DAV:" xmlns:oc="http://owncloud.org/ns" xmlns:nc="http://nextcloud.org/ns">
  <d:prop>
    <d:getlastmodified />
    <d:getetag />
    <d:getcontenttype />
    <d:resourcetype />
    <oc:fileid />
    <oc:permissions />
    <oc:size />
    <d:getcontentlength />
    <nc:has-preview />
    <oc:favorite />
    <oc:comments-unread />
    <oc:owner-display-name />
    <oc:share-types />
  </d:prop>
</d:propfind>
```

The following properties are supported:

-   `{DAV:}getlastmodified`{.sourceCode}
-   `{DAV:}getetag`{.sourceCode}
-   `{DAV:}getcontenttype`{.sourceCode}
-   `{DAV:}resourcetype`{.sourceCode}
-   `{DAV:}getcontentlength`{.sourceCode}
-   `{http://owncloud.org/ns}id`{.sourceCode} The fileid namespaced by
    the instance id, globally unique
-   `{http://owncloud.org/ns}fileid`{.sourceCode} The unique id for the
    file within the instance
-   `{http://owncloud.org/ns}favorite`{.sourceCode}
-   `{http://owncloud.org/ns}comments-href`{.sourceCode}
-   `{http://owncloud.org/ns}comments-count`{.sourceCode}
-   `{http://owncloud.org/ns}comments-unread`{.sourceCode}
-   `{http://owncloud.org/ns}owner-id`{.sourceCode} The user id of the
    owner of a shared file
-   `{http://owncloud.org/ns}owner-display-name`{.sourceCode} The
    display name of the owner of a shared file
-   `{http://owncloud.org/ns}share-types`{.sourceCode}
-   `{http://owncloud.org/ns}checksums`{.sourceCode}
-   `{http://owncloud.org/ns}has-preview`{.sourceCode}
-   `{http://owncloud.org/ns}size`{.sourceCode} Unlike
    `getcontentlength`{.sourceCode}, this property also works for
    folders reporting the size of everything in the folder.

\~\~\~\~ Getting properties for just the folder \~\~\~\~

You can request properties of a folder without also getting the folder
contents by adding a `Depth: 0`{.sourceCode} header to the request.

----Downloading files ----

A file can be downloaded by sending a `GET`{.sourceCode} request to the
WebDAV url of the file.

``` {.sourceCode .}
GET remote.php/dav/files/user/path/to/file
```

----Uploading files ----

A file can be uploading by sending a `PUT`{.sourceCode} request to the
file and sending the raw file contents as the request body.

``` {.sourceCode .}
PUT remote.php/dav/files/user/path/to/file
```

Any existing file will be overwritten by the request.

----Creating folders ([rfc4918](https://tools.ietf.org/html/rfc4918))
----

A folder can be created by sending a `MKCOL`{.sourceCode} request to the
folder.

``` {.sourceCode .}
MKCOL remote.php/dav/files/user/path/to/new/folder
```

----Deleting files and folders
([rfc4918](https://tools.ietf.org/html/rfc4918)) ----

A file or folder can be created by sending a `DELETE`{.sourceCode}
request to the file or folder.

``` {.sourceCode .}
DELETE remote.php/dav/files/user/path/to/file
```

When deleting a folder, it's contents will be deleted recursively.

----Moving files and folders
([rfc4918](https://tools.ietf.org/html/rfc4918)) ----

A file or folder can be moved by sending a `MOVE`{.sourceCode} request
to the file or folder and specifying the destination in the
`Destination`{.sourceCode} header as full url.

``` {.sourceCode .}
MOVE remote.php/dav/files/user/path/to/file
Destination: https://cloud.example/remote.php/dav/files/user/new/location
```

The overwrite behavior of the move can be controlled by setting the
`Overwrite`{.sourceCode} head to `T`{.sourceCode} or `F`{.sourceCode} to
enable or disable overwriting respectively.

----Copying files and folders
([rfc4918](https://tools.ietf.org/html/rfc4918)) ----

A file or folder can be copied by sending a `COPY`{.sourceCode} request
to the file or folder and specifying the destination in the
`Destination`{.sourceCode} header as full url.

``` {.sourceCode .}
COPY remote.php/dav/files/user/path/to/file
Destination: https://cloud.example/remote.php/dav/files/user/new/location
```

The overwrite behavior of the copy can be controlled by setting the
`Overwrite`{.sourceCode} head to `T`{.sourceCode} or `F`{.sourceCode} to
enable or disable overwriting respectively.

----Settings favorites ----

A file or folder can be marked as favorite by sending a
`PROPPATCH`{.sourceCode} request to the file or folder and setting the
`oc-favorite`{.sourceCode} property

``` {.sourceCode .xml}
PROPPATCH remote.php/dav/files/user/path/to/file
<?xml version="1.0"?>
<d:propertyupdate xmlns:d="DAV:" xmlns:oc="http://owncloud.org/ns">
  <d:set>
    <d:prop>
      <oc:favorite>1</oc:favorite>
    </d:prop>
  </d:set>
</d:propertyupdate>
```

Setting the `oc:favorite`{.sourceCode} property to 1 marks a file as
favorite, setting it to 0 un-marks it as favorite.

----Listing favorites ----

Favorites for a user can be retrieved by sending a `REPORT`{.sourceCode}
request and specifying `oc:favorite`{.sourceCode} as a filter

``` {.sourceCode .xml}
REPORT remote.php/dav/files/user/path/to/folder
<?xml version="1.0"?>
<oc:filter-files  xmlns:d="DAV:" xmlns:oc="http://owncloud.org/ns" xmlns:nc="http://nextcloud.org/ns">
     <oc:filter-rules>
         <oc:favorite>1</oc:favorite>
     </oc:filter-rules>
 </oc:filter-files>
```

File properties can be requested by adding a `<d:prop/>`{.sourceCode}
element to the request listing the requested properties in the same way
as it would be done for a `PROPFIND`{.sourceCode} request.

When listing favorites, the request will find all favorites in the
folder recursively, all favorites for a user can be found by sending the
request to `remote.php/dav/files/user`{.sourceCode}
