External API
============

Introduction
------------

The external API inside Nextcloud allows third party developers to
access data provided by Nextcloud apps. Nextcloud follows the
[OpenCloudMesh
specification](https://lukasreschke.github.io/OpenCloudMeshSpecification/)
(draft).

Usage
-----

### Registering Methods

Methods are registered inside the appinfo/routes.php by returning an
array holding the endpoint meta data.

``` {.sourceCode .php}
<?php

'ocs' => [
    // Apps
    ['name' => 'Bar#getFoo', 'url' => '/foobar', 'verb' => 'GET'],
];
```

### Returning Data

Once the API backend has matched your URL, your callable function as
defined in **BarController::getFoo** will be executed. The AppFramework
will make sure that send parameters are provided to the method based on
its declaration. To return data back to the client, you should return an
instance of (a subclass of) :phpOCP\\AppFramework\\Http\\Response,
typically :phpOCSResponse. The API backend will then use this to
construct the XML or JSON response.

### Authentication & Basics

Because REST is stateless you have to send user and password each time
you access the API. Therefore running Nextcloud **with SSL is highly
recommended**; otherwise **everyone in your network can log your
credentials**:

    https://user:password@example.com/ocs/v1.php/apps/yourapp

### Output

The output defaults to XML. If you want to get JSON append this to the
URL:

    ?format=json

Output from the application is wrapped inside a **data** element:

**XML**:

``` {.sourceCode .xml}
<?xml version="1.0"?>
<ocs>
 <meta>
  <status>ok</status>
  <statuscode>100</statuscode>
  <message/>
 </meta>
 <data>
   <!-- data here -->
 </data>
</ocs>
```

**JSON**:

``` {.sourceCode .js}
{
  "ocs": {
    "meta": {
      "status": "ok",
      "statuscode": 100,
      "message": null
    },
    "data": {
      // data here
    }
  }
}
```

### Statuscodes

The statuscode can be any of the following numbers:

-   **100** - successful
-   **996** - server error
-   **997** - not authorized
-   **998** - not found
-   **999** - unknown error

