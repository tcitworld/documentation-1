External Storage Authentication mechanisms
==========================================

Nextcloud storage backends accept one or more authentication schemes
such as passwords, OAuth, or token-based, to name a few examples. Each
authentication scheme may be implemented by multiple authentication
mechanisms. Different mechanisms require different configuration
parameters, depending on their behaviour.

![](images/authentication-types.png)

Special Mechanisms
------------------

The **None** authentication mechanism requires no configuration
parameters, and is used when a backend requires no authentication.

The **Built-in** authentication mechanism itself requires no
configuration parameters, but is used as a placeholder for legacy
storages that have not been migrated to the new system and do not take
advantage of generic authentication mechanisms. The authentication
parameters are provided directly by the backend.

Password-based Mechanisms
-------------------------

The **Username and password** mechanism requires a manually-defined
username and password. These get passed directly to the backend and are
specified during the setup of the mount point.

The **Log-in credentials, save in session** mechanism uses the Nextcloud
login credentials of the user to connect to the storage. These are not
stored anywhere on the server, but rather in the user session, giving
increased security. The drawbacks are that sharing is disabled when this
mechanism is in use, as Nextcloud has no access to the storage
credentials, and background file scanning does not work.

The **Log-in credentials, save in database** mechanism uses the
Nextcloud login credentials of the user to connect to the storage. These
are stored in the database encrypted with the shared secret. This allows
to share files from within this mount point.

The **User entered, store in database** mechanism work in the same way
as the "Username and password" mechanism but the credentials need to be
specified by each user individually. Before the first access to that
mount point the user will be prompted to enter the credentials.

The **Global credentials** mechanism uses the general input field for
"Global credentials" in the external storage settings section as source
for the credentials instead of individual credentials for a mount point.

Public-key Mechanisms
---------------------

Currently only the RSA mechanism is implemented, where a public/private
keypair is generated by Nextcloud and the public half shown in the GUI.
The keys are generated in the SSH format, and are currently 1024 bits in
length. Keys can be regenerated with a button in the GUI.

![](images/auth_rsa.png)

OAuth
-----

OAuth 1.0 and OAuth 2.0 are both implemented, but currently limited to
the Dropbox and Google Drive backends respectively. These mechanisms
require additional configuration at the service provider, where an app
ID and app secret are provided and then entered into Nextcloud. Then
Nextcloud can perform an authentication request, establishing the
storage connection.

![](images/dropbox-oc.png)