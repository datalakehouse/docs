Perform DBA-type tasks in datalakehouse for PostgreSQL
==============================================

datalakehouse doesn't allow superuser access to datalakehouse for PostgreSQL services. However, most DBA-type actions are still available through other methods.

``avnadmin`` user privileges
----------------------------

By default, in every PostgreSQL instance, an ``avnadmin`` database user is created, with permissions to perform most of the usual DB management operations. It can manage:

* Databases (``CREATE DATABASE``, ``DROP DATABASE``)
* Database users (``CREATE USER/ROLE``,`` DROP USER/ROLE``)
* Extensions (``CREATE EXTENSION``), you can also view the :doc:`list of available extensions <../reference/list-of-extensions>`
* Access permissions (``GRANT``, ``REVOKE``)
* Logical replication with the ``REPLICATION`` privilege

.. Tip::
    You can also manage databases and users in the datalakehouse web console or though our :doc:`REST API <../../../tools/api/index>`.

``datalakehouse_extras`` extension
--------------------------

The ``datalakehouse_extras`` extension, developed and maintained by datalakehouse, enables the ``avnadmin`` to perform superuser-like functionalities like:

* Manage `subscriptions <https://www.postgresql.org/docs/current/catalog-pg-subscription.html>`_
* Manage ``auto_explain`` `functionality <https://www.postgresql.org/docs/current/auto-explain.html>`_
* Manage `publications <https://www.postgresql.org/docs/current/sql-createpublication.html>`_
* :doc:`Claim public schema ownership <../howto/claim-public-schema-ownership>`

You can install the ``datalakehouse_extras`` extension executing the following command with the ``avnadmin`` user::

    CREATE EXTENSION datalakehouse_extras CASCADE;

For more information about ``datalakehouse_extras`` check the `GitHub repository <https://github.com/datalakehouse/datalakehouse-extras>`_ for the project.
