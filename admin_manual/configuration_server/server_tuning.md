Server Tuning
=============

Using cron to perform background jobs
-------------------------------------

See background\_jobs\_configuration for a description and the benefits.

Caching
-------

Caching improves performance by storing data, code, and other objects in
memory. Memory cache configuration for the Nextcloud server must be
installed and configured. See caching\_configuration.

Using MariaDB/MySQL instead of SQLite
-------------------------------------

MySQL or MariaDB are preferred because of the [performance limitations
of SQLite with highly concurrent
applications](http://www.sqlite.org/whentouse.html), like Nextcloud.

See the section
../configuration\_database/linux\_database\_configuration for how to
configure Nextcloud for MySQL or MariaDB. If your installation is
already running on SQLite then it is possible to convert to MySQL or
MariaDB using the steps provided in
../configuration\_database/db\_conversion.

Using Redis-based Transactional File Locking
--------------------------------------------

File locking is enabled by default, using the database locking backend.
This places a significant load on your database. See the section
../configuration\_files/files\_locking\_transactional for how to
configure Nextcloud to use Redis-based Transactional File Locking.

SSL / Encryption App
--------------------

SSL (HTTPS) and file encryption/decryption can be offloaded to a
processor's AES-NI extension. This can both speed up these operations
while lowering processing overhead. This requires a processor with the
[AES-NI instruction set](http://wikipedia.org/wiki/AES_instruction_set).

Here are some examples how to check if your CPU / environment supports
the AES-NI extension:

-   For each CPU core present: `grep flags /proc/cpuinfo` or as a
    summary for all cores: `grep -m 1 ^flags /proc/cpuinfo` If the
    result contains any `aes`, the extension is present.
-   Search eg. on the Intel web if the processor used supports the
    extension [Intel Processor Feature
    Filter](http://ark.intel.com/MySearch.aspx?AESTech=true) You may set
    a filter by `"AES New Instructions"` to get a reduced result set.
-   For versions of openssl &gt;= 1.0.1, AES-NI does not work via an
    engine and will not show up in the `openssl engine` command. It is
    active by default on the supported hardware. You can check the
    openssl version via `openssl  version -a`
-   If your processor supports AES-NI but it does not show up eg via
    grep or coreinfo, it is maybe disabled in the BIOS.
-   If your environment runs virtualized, check the virtualization
    vendor for support.

Enable HTTP2 for faster loading
-------------------------------

HTTP2 has [huge speed
improvements](https://www.troyhunt.com/i-wanna-go-fast-https-massive-speed-advantage/)
over HTTP with multiple request. Most [browsers already support HTTP2
over SSL (HTTPS)](http://caniuse.com/#feat=http2). So refer to your
server manual for guides on how to use HTTP2.

Enable PHP OPcache
------------------

The [OPcache](http://php.net/manual/en/intro.opcache.php) improves the
performance of PHP applications by caching precompiled bytecode. We
recommend at least following settings:

``` {.sourceCode .ini}
opcache.enable=1
opcache.enable_cli=1
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=10000
opcache.memory_consumption=128
opcache.save_comments=1
opcache.revalidate_freq=1
```

For more details check out the [official
documentation](http://php.net/manual/en/opcache.configuration.php) or
[this blog post about some recommended
settings](https://www.scalingphpbook.com/blog/2014/02/14/best-zend-opcache-settings.html).
