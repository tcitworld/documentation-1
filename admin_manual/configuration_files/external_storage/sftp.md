SFTP
====

Nextcloud's SFTP (FTP over an SSH tunne) backend supports both password
and public key authentication.

The **Host** field is required; a port can be specified as part of the
**Host** field in the following format: `hostname.domain:port`. The
default port is 22 (SSH).

For public key authentication, you can generate a public/private key
pair from your **SFTP with secret key login** configuration.

![](images/auth_mechanism.png)

After generating your keys, you need to copy your new public key to the
destination server to `.ssh/authorized_keys`. Nextcloud will then use
its private key to authenticate to the SFTP server.

The default **Remote Subfolder** is the root directory (`/`) of the
remote SFTP server, and you may enter any directory you wish.

See ../external\_storage\_configuration\_gui for additional mount
options and information.

See auth\_mechanisms for more information on authentication schemes.
