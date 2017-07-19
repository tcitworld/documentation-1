Language Configuration
======================

Default language
----------------

In normal cases Nextcloud will automatically detect the language of the
Web-GUI. If this does not work properly or you want to make sure that
Nextcloud always starts with a given language, you can set a
**default\_language** parameter in the config/config.php.

> **note**
>
> The default\_language paramenter is only used, when the browser does
> not send any language, and the user hasn't configured own language
> preferences.

    <?php

      "default_language" => "en",

Force language
--------------

If you want to force a specific language, users will no longer be able
to change their language in the personal settings. You can set a
**force\_language** parameter in the config/config.php.

    <?php

      "force_language" => "en",

If users shall be unable to change their language, but users have
different languages, this value can be set to `true` instead of a
language code.

> **note**
>
> Please check [Transifex language
> codes](https://www.transifex.com/explore/languages/) for the list of
> valid language codes.
