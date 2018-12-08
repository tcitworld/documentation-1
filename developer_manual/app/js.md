JavaScript
==========

The JavaScript files reside in the **js/** folder and should be included
in the template:

``` {.sourceCode .php}
<?php
// add one file
script('myapp', 'script');  // adds js/script.js

// add multiple files in the same app
script('myapp', array('script', 'navigation'));  //  adds js/script.js js/navigation.js

// add vendor files (also allows the array syntax)
vendor_script('myapp', 'script');  //  adds vendor/script.js
```

If the script file is only needed when the file list is displayed, you
should listen to the `OCA\Files::loadAdditionalScripts` event:

``` {.sourceCode .php}
<?php
$eventDispatcher = \OC::$server->getEventDispatcher();
$eventDispatcher->addListener('OCA\Files::loadAdditionalScripts', function() {
  script('myapp', 'script');  // adds js/script.js
  vendor_script('myapp', 'script');  //  adds vendor/script.js
});
```

Sending the CSRF token
----------------------

If any other JavaScript request library than jQuery is being used, the
requests need to send the CSRF token as an HTTP header named
**requesttoken**. The token is available in the global variable
**oc\_requesttoken**.

For AngularJS the following lines would need to be added:

``` {.sourceCode .js}
var app = angular.module('MyApp', []).config(['$httpProvider', function($httpProvider) {
    $httpProvider.defaults.headers.common.requesttoken = oc_requesttoken;
}]);
```

Generating URLs
---------------

To send requests to Nextcloud the base URL where Nextcloud is currently
running is needed. To get the base URL use:

``` {.sourceCode .js}
var baseUrl = OC.generateUrl('');
```

Full URLs can be generated by using:

``` {.sourceCode .js}
var authorUrl = OC.generateUrl('/apps/myapp/authors/1');
```

Extending core parts
--------------------

It is possible to extend components of the core web UI. The following
examples should show how this is possible.

### Extending the "new" menu in the files app

``` {.sourceCode .js}
var myFileMenuPlugin = {
    attach: function (menu) {
        menu.addMenuEntry({
            id: 'abc',
            displayName: 'Menu display name',
            templateName: 'templateName.ext',
            iconClass: 'icon-filetype-text',
            fileType: 'file',
            actionHandler: function () {
                console.log('do something here');
            }
        });
    }
};
OC.Plugins.register('OCA.Files.NewFileMenu', myFileMenuPlugin);
```

This will register a new menu entry in the "New" menu of the files app.
The method `attach()` is called once the menu is built. This usually
happens right after the click on the button.