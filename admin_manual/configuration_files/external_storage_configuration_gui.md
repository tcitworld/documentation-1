Configuring External Storage (GUI)
==================================

The External Storage Support application enables you to mount external
storage services and devices as secondary Nextcloud storage devices. You
may also allow users to mount their own external storage services.

Nextcloud 9.0 introduces a new set of
occ commands for managing external storage &lt;files\_external\_label&gt;.

Also new in 9.0 is an option for the Nextcloud admin to enable or
disable sharing on individual external mountpoints (see
external\_storage\_mount\_options\_label). Sharing on such mountpoints
is disabled by default.

Enabling External Storage Support
---------------------------------

> **warning**
>
> Enabling this app will disable the **Stay logged in** checkbox on the
> login page.

The External storage support application is enabled on your Apps page.

![](external_storage/images/enable-app.png)

Storage Configuration
---------------------

To create a new external storage mount, select an available backend from
the dropdown **Add storage**. Each backend has different required
options, which are configured in the configuration fields.

![](external_storage/images/add_storage.png)

Each backend may also accept multiple authentication methods. These are
selected with the dropdown under **Authentication**. Different backends
support different authentication mechanisms; some specific to the
backend, others are more generic. See external\_storage/auth\_mechanisms
for more detailed information.

When you select an authentication mechanism, the configuration fields
change as appropriate for the mechanism. The SFTP backend, for one
example, supports **username and password**, **Log-in credentials, save
in session**, and **RSA public key**.

![](external_storage/images/auth_mechanism.png)

Required fields are marked with a red border. When all required fields
are filled, the storage is automatically saved. A green dot next to the
storage row indicates the storage is ready for use. A red or yellow icon
indicates that Nextcloud could not connect to the external storage, so
you need to re-check your configuration and network availability.

If there is an error on the storage, it will be marked as unavailable
for ten minutes. To re-check it, click the colored icon or reload your
Admin page.

User and Group Permissions
--------------------------

A storage configured in a user's Personal settings is available only to
the user that created it. A storage configured in the Admin settings is
available to all users by default, and it can be restricted to specific
users and groups in the **Available for** field.

![](external_storage/images/applicable.png)

Mount Options
-------------

Hover your cursor to the right of any storage configuration to expose
the settings button and trashcan. Click the trashcan to delete the
mountpoint. The settings button allows you to configure each storage
mount individually with the following options:

-   Encryption
-   Previews
-   Enable Sharing
-   Filesystem check frequency (Never, Once per direct access)

The **Encryption** checkbox is visible only when the Encryption app is
enabled.

**Enable Sharing** allows the Nextcloud admin to enable or disable
sharing on individual mountpoints. When sharing is disabled the shares
are retained internally, so that you can re-enable sharing and the
previous shares become available again. Sharing is disabled by default.

![](external_storage/images/mount_options.png)

Using Self-Signed Certificates
------------------------------

When using self-signed certificates for external storage mounts the
certificate must be imported into the personal settings of the user.
Please refer to [Nextcloud HTTPS External
Mount](http://ownclouden.blogspot.de/2014/11/owncloud-https-external-mount.html)
for more information.

Available storage backends
--------------------------

The following backends are provided by the external storages app. Other
apps may provide their own backends, which are not listed here.

> **note**
>
> A non-blocking or correctly configured SELinux setup is needed for
> these backends to work. Please refer to the selinux-config-label.

Allow Users to Mount External Storage
-------------------------------------

Check **Enable User External Storage** to allow your users to mount
their own external storage services, and check the backends you want to
allow. Beware, as this allows a user to make potentially arbitrary
connections to other services on your network!

![](external_storage/images/user_mounts.png)

Adding Files to External Storages
---------------------------------

We recommend configuring the background job **Webcron** or **Cron** (see
../configuration\_server/background\_jobs\_configuration) to enable
Nextcloud to automatically detect files added to your external storages.

Nextcloud may not always be able to find out what has been changed
remotely (files changed without going through Nextcloud), especially
when it's very deep in the folder hierarchy of the external storage.

You might need to setup a cron job that runs
`sudo -u www-data php occ files:scan --all` (or replace "--all" with the
user name, see also ../configuration\_server/occ\_command) to trigger a
rescan of the user's files periodically (for example every 15 minutes),
which includes the mounted external storage.
