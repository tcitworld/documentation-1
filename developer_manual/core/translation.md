Translation
===========

Make text translatable
----------------------

In HTML or PHP wrap it like this
`<?php p($l->t('This is some text'));?>` or this
`<?php print_unescaped($l->t('This is some text'));?>`. For the right
date format use `<?php p($l->l('date', time()));?>`. Change the way
dates are shown by editing /core/l10n/l10n-{lang}.php.

To translate text in JavaScript use: `t('appname','text to translate');`

> **note**
>
> `print_unescaped()` should be preferred only if you would like to
> display HTML code. Otherwise, using `p()` is strongly preferred to
> escape HTML characters against XSS attacks.

You shall never split sentences!
--------------------------------

### Reason:

Translators lose the context and they have no chance to possibly
re-arrange words.

### Example:

``` {.sourceCode .php}
<?php p($l->t('Select file from')) . ' '; ?><a href='#' id="browselink"><?php p($l->t('local filesystem'));?></a><?php p($l->t(' or ')); ?><a href='#' id="cloudlink"><?php p($l->t('cloud'));?></a>
```

### Translators will translate:

-   Select file from
-   local filesystem
-   ' or "
-   cloud

Translating these individual strings results in `local filesystem` and
`cloud` losing case. The two white spaces surrounding `or` will get lost
while translating as well. For languages that have a different
grammatical order it prevents the translators from reordering the
sentence components.

### HTML on translation string:

HTML tags in translation strings is ugly but usually translators can
handle this.

### What about variable in the strings?

If you need to add variables to the translation strings do it like this:

``` {.sourceCode .php}
$l->t('%s is available. Get <a href="%s">more information</a>', array($data['versionstring'], $data['web']));
```

Automated synchronization of translations
-----------------------------------------

Multiple nightly jobs have been setup in order to synchronize
translations - it's a multi-step process:

1.  `perl l10n.pl read` will rescan all PHP and JavaScript files and
    generate the templates.
2.  The templates are pushed to
    [Transifex](https://www.transifex.com/nextcloud/) (tx push -s).
3.  All translations are pulled from
    [Transifex](https://www.transifex.com/nextcloud/) (tx pull -a).
4.  `perl l10n.pl write` will write the PHP files containing
    the translations.
5.  Finally the changes are pushed to Git.

### Please follow the steps below to add translation support to your app:

1.  Create a folder `l10n`.
2.  Create the file `ignorelist` which can contain files which shall not
    be scanned during step 4.
3.  Edit `l10n/.tx/config` and copy/paste a config section and adapt it
    by changing the app/folder name.
4.  Run `perl l10n.pl read` within the folder l10n.
5.  Add the newly created translation template
    (*l10n/Templates/&lt;appname&gt;.pot*) to Git and commit the
    changes above.
6.  After the next nightly sync job a new resource will appear on
    Transifex and from now on every night the latest translations
    will arrive.

**Caution: information below is in general not needed!**

Manual quick translation update:
--------------------------------

``` {.sourceCode .bash}
cd l10n/ && perl l10n.pl read && tx push -s && tx pull -a && perl l10n.pl write && cd ..
```

The translation script requires Locale::PO, installable via
`apt-get install liblocale-po-perl`.

Configure Transifex
-------------------

``` {.sourceCode .bash}
tx init

for resource in calendar contacts core files media gallery settings
do
tx set --auto-local -r nextcloud.$resource "<lang>/$resource.po" --source-language=en \
 --source-file "templates/$resource.pot" --execute
done
```
