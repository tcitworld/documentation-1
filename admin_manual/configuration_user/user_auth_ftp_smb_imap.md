User Authentication with IMAP, SMB, and FTP
===========================================

You may configure additional user backends in Nextcloud's configuration
config/config.php using the following syntax:

    <?php

    "user_backends" => array (
        0 => array (
                "class"     => ...,
                "arguments" => array (
                                  0 => ...
                                  ),
        ),
    ),

> **note**
>
> A non-blocking or correctly configured SELinux setup is needed for
> these backends to work. Please refer to the selinux-config-label.

Currently the “External user support” (user\_external) app, which you
need to enable first (See
../installation/apps\_management\_installation) provides the following
user backends:

IMAP
----

Provides authentication against IMAP servers

-   **Class:** OC\_User\_IMAP
-   **Arguments:** a mailbox string as defined [in the PHP
    documentation](http://www.php.net/manual/en/function.imap-open.php)
-   **Dependency:** php-imap (See ../installation/source\_installation)
-   **Example:**

<!-- -->

    <?php

    "user_backends" => array (
        0 => array (
                "class"     => "OC_User_IMAP",
                "arguments" => array (
                                  0 => '{imap.gmail.com:993/imap/ssl}'
                                  ),
        ),
    ),

SMB
---

Provides authentication against Samba servers

-   **Class:** OC\_User\_SMB
-   **Arguments:** the samba server to authenticate against
-   **Dependency:** PHP smbclient module or smbclient
    (see ../configuration\_files/external\_storage/smb)
-   **Example:**

<!-- -->

    <?php

    "user_backends" => array (
        0 => array (
                "class"     => "OC_User_SMB",
                "arguments" => array (
                                  0 => 'localhost'
                                  ),
        ),
    ),

FTP
---

Provides authentication against FTP servers

-   **Class:** OC\_User\_FTP
-   **Arguments:** the FTP server to authenticate against
-   **Dependency:** php-ftp (See ../installation/source\_installation)
-   **Example:**

<!-- -->

    <?php

    "user_backends" => array (
        0 => array (
                "class"     => "OC_User_FTP",
                "arguments" => array (
                                  0 => 'localhost'
                                  ),
        ),
    ),
