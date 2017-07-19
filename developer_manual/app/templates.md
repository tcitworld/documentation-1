Templates
=========

Nextcloud provides its own templating system which is basically plain
PHP with some additional functions and preset variables. All the
parameters which have been passed from the
controller &lt;controllers&gt; are available in an array called
**\$\_\[\]**, e.g.:

    array('key' => 'something')

can be accessed through:

    $_['key']

> **note**
>
> To prevent XSS the following PHP **functions for printing are
> forbidden: echo, print() and &lt;?=**. Instead use the **p()**
> function for printing your values. Should you require unescaped
> printing, **double check for XSS** and use: :phpprint\_unescaped.

Printing values is done by using the **p()** function, printing HTML is
done by using **print\_unescaped()**

templates/main.php

``` {.sourceCode .php}
<?php foreach($_['entries'] as $entry){ ?>
  <p><?php p($entry); ?></p>
<?php
}
```

Including templates
-------------------

Templates can also include other templates by using the
**\$this-&gt;inc('templateName')** method.

``` {.sourceCode .php}
<?php print_unescaped($this->inc('sub.inc')); ?>
```

The parent variables will also be available in the included templates,
but should you require it, you can also pass new variables to it by
using the second optional parameter as array for **\$this-&gt;inc**.

templates/sub.inc.php

``` {.sourceCode .php}
<div>I am included, but I can still access the parents variables!</div>
<?php p($_['name']); ?>

<?php print_unescaped($this->inc('other_template', array('variable' => 'value'))); ?>
```

Including CSS and JavaScript
----------------------------

To include CSS or JavaScript use the **style** and **script** functions:

``` {.sourceCode .php}
<?php
script('myapp', 'script');  // add js/script.js
style('myapp', 'style');  // add css/style.css
```

Including images
----------------

To generate links to images use the **image\_path** function:

``` {.sourceCode .php}
<img src="<?php print_unescaped(image_path('myapp', 'app.png')); ?>" />
```
