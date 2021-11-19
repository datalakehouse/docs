datalakehouse API overview
==================

The datalakehouse API allows you to perform any tasks on datalakehouse from a client of your choice.

API quickstart
--------------

* You will need an authentication token from the `profile section of your datalakehouse console <https://console.datalakehouse.io/profile/auth>`_.

* Check the `API docs and OpenAPI spec <https://api.datalakehouse.io/doc/>`_ for the available endpoints.


Calling the datalakehouse API
---------------------

The datalakehouse API is a traditional HTTP API. All our own tools, such as the `web console <https://console.datalakehouse.io>`_ and ``avn`` CLI use this API.

.. mermaid::

    sequenceDiagram
        participant Client
        participant datalakehouse

        Client->>datalakehouse: Request with access token
        datalakehouse->>Client: Response {JSON}

Authorization
'''''''''''''

Obtain an authentication token from your `datalakehouse console <https://console.datalakehouse.io/profile/auth>`_. This will be sent as an ``Authorization`` header, like this::

    Authorization: Bearer <TOKEN>

Handling JSON responses
'''''''''''''''''''''''

The datalakehouse API returns information in JSON format, sometimes a lot of information. This is perfect for machines but not ideal for humans. We like to use a tool like `jq <https://stedolan.github.io/jq/>`_ to make things easier to read and manipulate.

datalakehouse API and Postman
'''''''''''''''''''''''

If you prefer an even more friendly tool, we have a blog post about `using Postman with datalakehouse's API <https://datalakehouse.io/blog/your-first-datalakehouse-api-call>`_ including how to import a Postman collection and spin up datalakehouse services with Postman.

