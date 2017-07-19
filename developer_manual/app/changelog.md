Changelog
=========

Deprecations
------------

This is a deprecation roadmap which lists all current deprecation
targets and will be updated from release to release. This lists the year
when a specific method or class will be removed.

> **note**
>
> Deprecations on interfaces also affect the implementing classes!

### 2018

-   **OCP\\App::setActiveNavigationEntry** has been deprecated in favour
    of **\\OCP\\INavigationManager**
-   **OCP\\BackgroundJob::registerJob** has been deprecated in favour of
    **OCP\\BackgroundJob\\IJobList**
-   **OCP\\Contacts** functions has been deprecated in favour of
    **\\OCP\\Contacts\\IManager**
-   **OCP\\DB** functions have been deprecated in favour of the ones in
    **\\OCP\\IDBConnection**
-   **OCP\\Files::tmpFile** has been deprecated in favour of
    **\\OCP\\ITempManager::getTemporaryFile**
-   **OCP\\Files::tmpFolder** has been deprecated in favour of
    **\\OCP\\ITempManager::getTemporaryFolder**
-   **\\OCP\\IServerContainer::getDb** has been deprecated in favour of
    **\\OCP\\IServerContainer::getDatabaseConnection**
-   **\\OCP\\IServerContainer::getHTTPHelper** has been deprecated in
    favour of **\\OCP\\Http\\Client\\IClientService**
-   Legacy applications not using the AppFramework are now likely to use
    the deprecated **OCP\\JSON** and **OCP\\Response** code:
    -   **\\OCP\\JSON** has been completely deprecated in favour of
        the AppFramework. Developers shall use the AppFramework instead
        of using the legacy **OCP\\JSON** code. This allows testable
        controllers and is highly encouraged.
    -   **\\OCP\\Response** has been completely deprecated in favour of
        the AppFramework. Developers shall use the AppFramework instead
        of using the legacy **OCP\\JSON** code. This allows testable
        controllers and is highly encouraged.
-   Diverse **OCP\\Users** function got deprecated in favour of
    **OCP\\IUserManager**:

    -   **OCP\\Users::getUsers** has been deprecated in favour of
        **OCP\\IUserManager::search**
    -   **OCP\\Users::getDisplayName** has been deprecated in favour of
        **OCP\\IUserManager::getDisplayName**
    -   **OCP\\Users::getDisplayNames** has been deprecated in favour of
        **OCP\\IUserManager::searchDisplayName**

    \* **OCP\\Users::userExists** has been deprecated in favour of
    **OCP\\IUserManager::userExists**
-   Various static **OCP\\Util** functions have been deprecated:
    -   **OCP\\Util::linkToRoute** has been deprecated in favour of
        **\\OCP\\IURLGenerator::linkToRoute**
    -   **OCP\\Util::linkTo** has been deprecated in favour of
        **\\OCP\\IURLGenerator::linkTo**
    -   **OCP\\Util::imagePath** has been deprecated in favour of
        **\\OCP\\IURLGenerator::imagePath**
    -   **OCP\\Util::isValidPath** has been deprecated in favour of
        **\\OCP\\IURLGenerator::imagePath**
-   [OCP\\AppFramework\\IAppContainer](https://github.com/nextcloud/server/blob/stable9/lib/public/appframework/iappcontainer.php):
    methods **getCoreApi** and **log**
-   [OCP\\AppFramework\\IApi](https://github.com/nextcloud/server/blob/stable9/lib/public/appframework/iapi.php):
    full class

### 2017

-   **OCP\\IDb**: This interface and the implementing classes will be
    removed in favor of **OCP\\IDbConnection**. Various layers in
    between have also been removed to be consistent with the
    PDO classes. This leads to the following changes:

> -   Replace all calls on the db using **getInsertId** with
>     **lastInsertId**
> -   Replace all calls on the db using **prepareQuery** with
>     **prepare**
> -   The **\_\_construct** method of **OCP\\AppFramework\\Db\\Mapper**
>     no longer requires an instance of **OCP\\IDb** but an instance of
>     **OCP\\IDbConnection**
> -   The **execute** method on **OCP\\AppFramework\\Db\\Mapper** no
>     longer returns an instance of **OC\_DB\_StatementWrapper** but an
>     instance of **PDOStatement**

### 2016

-   The following methods have been moved into the
    **OCP\\Template::&lt;method&gt;** class instead of being namespaced
    directly:

> -   **OCP\\image\_path**
> -   **OCP\\mimetype\_icon**
> -   **OCP\\preview\_icon**
> -   **OCP\\publicPreview\_icon**
> -   **OCP\\human\_file\_size**
> -   **OCP\\relative\_modified\_date**
> -   **OCP\\html\_select\_options**

-   **OCP\\simple\_file\_size** has been deprecated in favour of
    **OCP\\Template::human\_file\_size**
-   The **OCP\\PERMISSION\_&lt;permission&gt;** and
    **OCP\\FILENAME\_INVALID\_CHARS** have been moved to
    **OCP\\Constants::&lt;old name&gt;**
-   The **OC\_GROUP\_BACKEND\_&lt;method&gt;** and
    **OC\_USER\_BACKEND\_&lt;method&gt;** have been moved to
    **OC\_Group\_Backend::&lt;method&gt;** and
    **OC\_User\_Backend::&lt;method&gt;** respectively
-   [OCP\\AppFramework\\Controller](https://github.com/nextcloud/server/blob/stable9/lib/public/appframework/controller.php):
    methods **params**, **getParams**, **method**, **getUploadedFile**,
    **env**, **cookie**, **render**

### 2015

-   [\\OC\\Preferences](https://github.com/nextcloud/server/commit/909a53e087b7815ba9cd814eb6c22845ef5b48c7)
    and
    [\\OC\_Preferences](https://github.com/nextcloud/server/commit/4df7c0a1ed52ed1922116686cb5ad8da2544c997)

