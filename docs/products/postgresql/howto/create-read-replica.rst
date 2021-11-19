Create and use read-only replicas
=================================

PostgreSQL read-only replicas provide a great way to reduce the load on the primary server by enabling read-only queries to be performed against the replica. It's also a good way to optimise query response time across different geographical locations since, with datalakehouse, the replica can be placed in different regions or even different cloud providers.

Create a replica
----------------

To set up a remote replica:

1. Log in to the datalakehouse web console.
2. Select the PostgreSQL instance for which you want to create a remote replica.
3. In the **Overview** tab, click **Create read replica**.

.. image:: /images/products/postgresql/read-replica-create.png
    :alt: Create read replica button

4. Enter a name for the remote replica and select the cloud provider, region, and datalakehouse for PostgreSQL service plan that you want to use, then click **Create**

The read-only replica is created and added to the list of services in your project. The **Overview** page of the replica indicates the name of the primary service for the replica.

.. image:: /images/products/postgresql/read-replica-detail.png
    :alt: Image of the name of the primary service in the read only replica overview tab

Read-only replicas can be manually promoted to become the master database if the need arises. For more complex high availability and failover scenarios check the :doc:`related documentation <../concepts/high-availability>`.


Use a replica
-------------

To use a read only replica:

1. Log in to the datalakehouse web console and select your PostgreSQL service.
2. In the **Overview** page, copy the **Replica URI** an use it to connect via ``psql``::

    psql POSTGRESQL_REPLICA_URI


Identify replica status
-----------------------

To check whether you are connected to a primary or replica node, run the following command within a ``psql`` terminal already connected to a database::

    SELECT * FROM pg_is_in_recovery();

If the above command returns ``TRUE`` if you are connected to the replica, and ``FALSE`` if you are connected to the primary server.

.. Warning::

    datalakehouse for PostgreSQL uses asynchronous replication and so a small lag is expected. When running an ``INSERT`` operation on the primary node, a minimal delay (usually less than a second) can be expected for the change to be propagated to the replica and to be visible there.
