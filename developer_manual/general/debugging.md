Debugging
=========

Debug mode
----------

When debug mode is enabled in Nextcloud, a variety of debugging features
are enabled - see debugging documentation. Set `debug` to `true` in
/config/config.php to enable it:

``` {.sourceCode .php}
<?php
$CONFIG = array (
    'debug' => true,
    ... configuration goes here ...
);
```

Identifying errors
------------------

Nextcloud uses custom error PHP handling that prevents errors being
printed to Web server log files or command line output. Instead, errors
are generally stored in Nextcloud's own log file, located at:
/data/nextcloud.log

Debugging variables
-------------------

You should use exceptions if you need to debug variable values manually,
and not alternatives like trigger\_error() (which may not be logged).

e.g.:

``` {.sourceCode .php}
<?php throw new \Exception( "\$user = $user" ); // should be logged in Nextcloud ?>
```

not:

``` {.sourceCode .php}
<?php trigger_error( "\$user = $user" ); // may not be logged anywhere ?>
```

To disable custom error handling in Nextcloud (and have PHP and your Web
server handle errors instead), see Debug mode.

Using a PHP debugger (XDebug)
-----------------------------

Using a debugger connected to PHP allows you to step through code line
by line, view variables at each line and even change values while the
code is running. The de-facto standard debugger for PHP is XDebug,
available as an installable package in many distributions. It just
provides the PHP side however, so you will need a frontend to actually
control XDebug. When installed, it needs to be enabled in php.ini, along
with some parameters to enable connections to the debugging interface:

``` {.sourceCode .ini}
zend_extension=/usr/lib/php/modules/xdebug.so
xdebug.remote_enable=on
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9000
xdebug.remote_handler=dbgp
```

XDebug will now (when activated) try to connect to localhost on port
9000, and will communicate over the standard protocol DBGP. This
protocol is supported by many debugging interfaces, such as the
following popular ones:

-   vdebug - Multi-language DBGP debugger client for Vim
-   SublimeTextXdebug - XDebug client for Sublime Text
-   PHPStorm - in-built DBGP debugger

For further reading, see the XDebug documentation:
<http://xdebug.org/docs/remote>

Once you are familiar with how your debugging client works, you can
start debugging with XDebug. To test Nextcloud through the web interface
or other HTTP requests, set the `XDEBUG_SESSION_START` cookie or POST
parameter. Alternatively, there are browser extensions to make this
easy:

-   The Easiest XDebug (Firefox):
    <https://addons.mozilla.org/en-US/firefox/addon/the-easiest-xdebug/>
-   XDebug Helper (Chrome):
    <https://chrome.google.com/extensions/detail/eadndfjplgieldjbigjakmdgkmoaaaoc>

For debugging scripts on the command line, like `occ` or unit tests, set
the `XDEBUG_CONFIG` environment variable.

Debugging Javascript
--------------------

By default all Javascript files in Nextcloud are minified (compressed)
into a single file without whitespace. To prevent this, see Debug mode.

Debugging HTML and templates
----------------------------

By default Nextcloud caches HTML generated by templates. This may
prevent changes to app templates, for example, from being applied on
page refresh. To disable caching, see Debug mode.

Using alternative app directories
---------------------------------

It may be useful to have multiple app directories for testing purposes,
so you can conveniently switch between different versions of
applications. See the configuration file documentation for details.