App Development
===============

Intro
-----

Before you start, please check if there already is a similar app in the
[App Store](https://apps.nextcloud.com) or the [GitHub
organisation](https://github.com/nextcloud/) that you could contribute
to. Also, feel free to communicate your idea and plans in the
[forum](https://help.nextcloud.com/) so other contributors might join
in.

Then, please make sure you have set up a development environment:

-   ../general/devenv

Before starting to write an app please read the security and coding
guidelines:

-   ../general/security
-   ../general/codingguidelines

After this you can start with the tutorial

-   tutorial

Once you are ready for publishing, check out the app store process:

-   publishing

For enhanced security it is also possible to sign your code:

-   code\_signing

App development
---------------

Take a look at the changes in this version:

-   changelog

Create a new app:

-   startapp

Inner parts of an app:

-   init
-   info
-   classloader

### Requests

How a request is being processed:

-   request
-   routes
-   middleware
-   container
-   controllers | api

### View

The app's presentation layer:

-   templates
-   js
-   css
-   l10n
-   theming

### Storage

Create database tables, run Sql queries, store/retrieve configuration
information and access the filesystem:

-   schema
-   database
-   configuration
-   filesystem

### Authentication & Users

Creating, deleting, updating, searching, login and logout:

-   users

Writing a two-factor auth provider:

-   two-factor-provider

### Hooks

Listen on events like user creation and execute code:

-   hooks

### Background Jobs

Periodically run code in the background:

-   backgroundjobs

### Settings

An app can register both admin settings as well as personal settings:

-   settings

### Logging

Log to the data/nextcloud.log:

-   logging

### Testing

Write automated tests to ensure stability and ease maintenance:

-   testing

### PHPDoc Class Documentation

Nextcloud class and function documentation:

-   [Nextcloud App API](https://api.owncloud.org/namespaces/OCP.html)

