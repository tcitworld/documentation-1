iOS - Synchronize iPhone/iPad
=============================

Calendar
--------

1.  Open the settings application.
2.  Select Mail, Contacts, Calendars.
3.  Select Add Account.
4.  Select Other as account type.
5.  Select Add CalDAV account.
6.  For server, type
    `example.com/remote.php/dav/principals/users/USERNAME/`
7.  Enter your user name and password.
8.  Select Next.
9.  If your server does not support SSL, a warning will be displayed.
    Select Continue.
10. If the iPhone is unable to verify the account information perform
    the following steps:
    -   Select OK.
    -   Select advanced settings.
    -   If your server does not support SSL, make sure Use SSL is set
        to OFF.
    -   Change port to 80.
    -   Go back to account information and hit Save.

Your calendar will now be visible in the Calendar application

Address book
------------

1.  Open the settings application.
2.  Select Mail, Contacts, Calendars.
3.  Select Add Account.
4.  Select Other as account type.
5.  Select Add CardDAV account.
6.  For server, type
    `example.com/remote.php/dav/principals/users/USERNAME/`
7.  Enter your user name and password.
8.  Select Next.
9.  If your server does not support SSL, a warning will be displayed.
    Select Continue.
10. If the iPhone is unable to verify the account information perform
    the following:
    -   Select OK.
    -   Select advanced settings.
    -   If your server does not support SSL, make sure Use SSL is set
        to OFF.
    -   Change port to 80.
    -   Go back to account information and hit Save.

Now should now find your contacts in the address book of your iPhone. If
it's still not working, have a look at the troubleshooting and
[Troubleshooting Contacts &
Calendar](https://docs.nextcloud.org/server/12/admin_manual/issues/index.html#troubleshooting-contacts-calendar)
guides.
