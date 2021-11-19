DLH API overview
==================

The DLH API allows you to perform any tasks on DLH from a client of your choice.

API quickstart
--------------

* You will need an authentication token from the `profile section of your DLH console <https://console.DLH.io/profile/auth>`_.

* Check the `API docs and OpenAPI spec <https://api.DLH.io/doc/>`_ for the available endpoints.


Calling the DLH API
---------------------

The DLH API is a traditional HTTP API. All our own tools, such as the `web console <https://console.DLH.io>`_ and ``avn`` CLI use this API.

.. mermaid::

    sequenceDiagram
        participant Client
        participant DLH

        Client->>DLH: Request with access token
        DLH->>Client: Response {JSON}

Authorization
'''''''''''''

Obtain an authentication token from your `DLH console <https://console.DLH.io/profile/auth>`_. This will be sent as an ``Authorization`` header, like this::

    Authorization: Bearer <TOKEN>

Handling JSON responses
'''''''''''''''''''''''

The DLH API returns information in JSON format, sometimes a lot of information. This is perfect for machines but not ideal for humans. We like to use a tool like `jq <https://stedolan.github.io/jq/>`_ to make things easier to read and manipulate.

DLH API and Postman
'''''''''''''''''''''''

If you prefer an even more friendly tool, we have a blog post about `using Postman with DLH's API <https://DLH.io/blog/your-first-DLH-api-call>`_ including how to import a Postman collection and spin up DLH services with Postman.

