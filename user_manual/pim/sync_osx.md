Synchronizing with OS X
=======================

To use Nextcloud with iCal you will need to use the following URL:

    https://example.com/remote.php/dav/principals/users/USERNAME/

The setup is basically the same as with iOS using the path
`https://example.com/remote.php/dav/principals/users/USERNAME/` to sync
with Nextcloud. For OS X 10.7 Lion and 10.8 Mountain Lion everything
works fine, but OS X 10.6 (Snow Leopard) and older needs some fiddling
to work. A user contributed the following:

\#. Make sure, "Addressbook" is not running. If it is, select the
windows and press Command + Q to terminate it. \#. Navigate to
**/Users/YOUR\_USERNAME/Library/Application
Support/AddressBook/Sources**. If you already have some kind of
addressbook set up, it is likely you will see some folders named like
this **BEA92826-FBF3-4E53-B5C6-ED7C2B454430**. Note down what folders
there are now and leave the window open. \#. Open "Addressbook" and try
to add a new CardDav addressbook. At this point, it does not matter what
information you enter. It will come up with the same error message you
mentioned before when you click "Create". Ignore it and click "Create"
again. A non-functional addressbook will be added. \#. Close
"Addressbook" again using Command + Q \#. Go back to the folder window
from step 2. You will now see a newly created folder with another long
string as its name. \#. Navigate to the newly created folder and edit
the **Configuration.plist** with your favorite text editor. \#. Search
for a section looking like this:

    <key>servername</key> <string>https://:0(null)</string> <key>username</key> <string>Whatever_you_entered_before</string>

8.  Make it look like this. Please note that the :443 after
    **example.com** is important:

        <key>servername</key <string>https://example.com:443/nextcloud/remote.php/dav/principals/users/USERNAME</string> <key>username</key <string>username</string>

9.  Save the file and open addressbook again. It will not work yet.
10. Open the preferences for your Nextcloud CardDAV-Account and enter
    your password.
11. You may have to restart addressbook once more. After this, it
    should work.

If it's still not working, have a look at the troubleshooting and
[Troubleshooting Contacts &
Calendar](https://docs.nextcloud.org/server/12/admin_manual/issues/index.html#troubleshooting-contacts-calendar)
guides.

There is also an easy
[HOWTO](https://forum.owncloud.org/viewtopic.php?f=3&t=132) in the
forum.