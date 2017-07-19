Theming support
===============

The Nextcloud theming app offers some tools for app developers to ensure
that apps also match the themed look.

CSS classes
-----------

-   **.nc-theming-main-background** Background in theming color
-   **.nc-theming-main-text** Text in theming color
-   **.nc-theming-contrast** Text in white/black color to be shown in
    front of the theming color

JavaScript
----------

When the theming app is enabled, it provides the **OCA.Theming** object.
It can be used to handle themed instances differently.

``` {.sourceCode .javascript}
if(OCA.Theming) {
  $('.myapp-element').animate({backgroundColor:OCA.Theming.color});
}
```

The following information is available:

-   **OCA.Theming.color** Main color
-   **OCA.Theming.inverted** Will be true on bright theming colors to
    get contrast with text
-   **OCA.Theming.name** Instance name
-   **OCA.Theming.slogan** Instance slogan
-   **OCA.Theming.url** Instance web address

Icons
-----

The theming app will automatically generate favicons and home screen
icons for each app by using the icon img/app.svg inside of the app
folder. Any custom favicon set by an app will only be visible when the
theming app is disabled.
