Configure ACL permissions in datalakehouse for Redis
==============================================

Use the datalakehouse console or the datalakehouse client to create custom Access Control Lists (ACLs). 

Redis uses `ACLs <https://redis.io/topics/acl>`_ to restrict the usage of commands and keys available for connecting for a specific username and password. datalakehouse for Redis, however, does not allow use of the  `ACL * <https://redis.io/commands/acl-list>`_ commands directly in order to guarantee the reliability of replication, configuration management, or backups for disaster recovery for the default user. You can use the console or the client to create custom ACLs instead.


Create an ACL using the datalakehouse console
-------------------------------------

1. Log in to the `datalakehouse web console <https://console.datalakehouse.io/>`_.

2. From the *Services* page, select the Redis service you want to create an ACL for.

   The *Overview* page for the service opens.

3. Click the **Users and ACL**.

4. Click **+ Add Service User**. 

   The *New Redis User* pop-up opens.

5. Create a user, and define which **Keys**, **Categories**, **Commands** or **Channels** the user can access. 

   In this example, the ``test`` user can only retrieve keys with the pattern ``mykeys.*``.

   .. image:: /images/products/redis/redis-acl.png
       :alt: Screenshot of the ACL configuration screen

6. Click **Save**. 


Create an ACL using the datalakehouse CLI
---------------------------------

1. Set up the :doc:`CLI tool </docs/tools/cli>` if you don't have it already.

2. Create a user for ``mynewuser`` with read-only access to the ``mykeys.*`` keys::

    avn service user-create --project myproject myservicename --username mynewuser --redis-acl-keys 'mykeys.*' --redis-acl-commands '+get' --redis-acl-categories ''

3. Confirm the ACL is applied by connecting to the service using the new username and password::

    redis-cli --user mynewuser --pass ... --tls -h myservice-myproject.datalakehousecloud.com -p 12719

    myservice-myproject.datalakehousecloud.com:12719> get mykeys.hello
    (nil)
    myservice-myproject.datalakehousecloud.com:12719> set mykeys.hello world
    (error) NOPERM this user has no permissions to run the 'set' command or its subcommand
