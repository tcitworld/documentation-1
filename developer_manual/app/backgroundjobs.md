Background Jobs (Cron)
======================

Background/cron jobs are usually registered in the appinfo/app.php by
using the **addRegularTask** method, the class and the method to run:

``` {.sourceCode .php}
<?php
\OCP\Backgroundjob::addRegularTask('\OCA\MyApp\Cron\SomeTask', 'run');
```

The class for the above example would live in cron/sometask.php. Try to
keep the method as small as possible because its hard to test static
methods. Simply reuse the app container and execute a service that was
registered in it:

``` {.sourceCode .php}
<?php
namespace OCA\MyApp\Cron;

use \OCA\MyApp\AppInfo\Application;

class SomeTask {

    public static function run() {
        $app = new Application();
        $container = $app->getContainer();
        $container->query('SomeService')->run();
    }

}
```

Don't forget to configure the cron service on the server by executing:

    sudo crontab -u http -e

where **http** is your Web server user, and add:

    */15  *  *  *  * php -f /srv/http/nextcloud/cron.php
