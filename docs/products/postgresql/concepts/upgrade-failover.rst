Upgrade and failover procedures
===============================

Aiven for PostgreSQL Business and Premium plans include **standby read-replica** servers. If the primary server fails, a standby replica server is automatically promoted as new primary server.

.. Warning::
    Standby read-replica servers available on PostgreSQL Business and Premium plans are substantially different from manually created read-replica services since the latter are not promoted if the primary server fails.

There are two distinct cases when failover or switchover occurs:

1. Uncontrolled primary/replica disconnection
2. Controlled switchover during rolling-forward upgrades

.. Warning::
    For Hobbyist and Startup plans, due to missing standby read-replica servers, uncontrolled disconnections can only be mitigated by restoring data from a backup, and can result in data loss of the database changes since the latest available backup.

.. _Failover PGUncontrolled:

Uncontrolled primary/replica disconnection
------------------------------------------

When a server unexpectedly disconnects, there is no certain way to know whether it really disappeared or whether there is a temporary glitch in the cloud provider's network. Aiven's management platform has different procedures in case of primary or replica nodes disconnections.

Primary server disconnection
""""""""""""""""""""""""""""

If the **primary** server disappears, Aiven's management platform uses a **60-second timeout** before marking the server as down and promoting a replica server as new primary. During this 60-second timeout, the master is unavailable (``servicename.aivencloud.com`` does not respond), and ``replica.servicename.aivencloud.com`` works fine (in read-only mode).

After the replica promotion, ``servicename.aivencloud.com`` would point to the new primary server, while ``replica.servicename.aivencloud.com`` becomes unreachable. Finally, a new replica server is created, and after the synchronisation with the primary, the  ``replica.servicename.aivencloud.com`` DSN is switched to point to the new replica server.

Replica server disconnection
""""""""""""""""""""""""""""

If the **replica** server disappears, Aiven's management platform uses a **300-second timeout** before marking the server as down and creating a new replica server. During this period, the DNS ``replica.servicename.aivencloud.com`` points to the disappeared server that might not serve queries anymore. The DNS record pointing to the primary server (``servicename.aivencloud.com``) remains unchanged.

If the replica server does not come back online during these 300 seconds, ``replica.servicename.aivencloud.com`` is pointed to the primary server until a new replica server is fully functional.

Controlled switchover during upgrades or migrations
---------------------------------------------------

During maintenance updates, cloud migrations, or plan changes, the below procedure is followed:

1. For each of the **replica** nodes (available only on Business and Premium plans), a new server is created, and data restored from a backup. Then the new server starts following the existing primary server. After the new server is up and running and data up-to-date, ``replica.servicename.aivencloud.com`` DNS entry is changed to point to it, and the old replica server is deleted.

2. An additional server is created, and data restored from a backup. Then the new server is synced up to the old primary server.

3. Cluster replication is changed to **quorum commit synchronous** to avoid data loss when changing primary server.

.. Note::
    At this stage, one extra server running: the old primary server, and N+1 replica servers (2 for Business and 3 for Premium plans).

3. The old primary server is scheduled for termination, and one of the new replica servers is immediately promoted as a primary server. ``servicename.aivencloud.com`` DSN is updated to point to the new primary server. The new primary server is removed from the ``replica.servicename.aivencloud.com`` DSN record.

.. Note::
    The old primary server is kept alive for a short period of time with a TCP forwarding setup pointing to the new primary server allowing clients to connect before learning the new IP address.
