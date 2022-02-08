# Basic SQL Server setup

### Let's connect your SQL Server database!

Go ahead and gather the basic details:

* Database host or IP Address
* Database port # (default is 1433)

**SQL Server Specifications Required:**

* SQL Server versions 2012-2019 (talk w/ support if other versions needed)
* Determine which way to connect: TLS or SSH Tunneling
  * _As of July 2021 only the default TLS approach is available. This is just like if you were to connect from SQL Server Management Studio for example._
  * _Microsoft has some good_ [_instructions on TLS setup_](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine?view=sql-server-ver15#transport-layer-security-tls)
* Firewalls on your database server should allow incoming connections through the public internet on your SQL Server port (typically 1433 unless your network guys have changed it).  Be sure to [whitelist our DataLakeHouse.io IP addresses](https://datalakehouse.io/whitelist-ip-addresses) for your database server network access.

### Instructions (Basic Connection Setup)

Scroll down to ensure you review all steps, as needed...

Remember DataLakeHouse.io connects to your database instance with credentials supplied by you. We store your credentials securely with our bank-grade protocols.

1. **Create a DataLakeHouse user on the SQL Server database**
   * Connect to the SQL Server database in question with your admin (usually sa) user.
   *   Create a user for DataLakeHouse using the following SQL logic replacing \<database> with the name of your database, \<username> with you a user name that you choose (we recommend 'datalakehouse\_ro' to signify a read-only user), and choose a good password that complies with your security policies.&#x20;

       ```
         USE [<database>];
           CREATE LOGIN <username> WITH PASSWORD = '<password>';
           CREATE USER <username> FOR LOGIN <username>;
       ```
2. **Grant the new user Permissions on Database, Schemas, Tables**
   * The new user needs **SELECT** permissions for the database, schemas, tables or any specified columns that will be synchronized.
     * We recommend granting SELECT access to everything in your specified database for this connection
     *   _Remember if you need to synch more databases you need to created a separate source connection._

         ```
           GRANT SELECT ON DATABASE::<database> to <username>;
         ```
   * Save the credentials somewhere and use them in the next steps
   * Please see other GRANT SELECT on schema and tables in our documentation if you need to get more granular for security purposes.
3. \*\*Enter your Credentials and Other Information in the Fields \*\*
   * Enter in the _**Name/Alias**_ field, the name you'll use within datalakehouse.io to differentiate this connection from others
   * Enter in the _**Target Schema Prefix**_ field, is the prefix of schema(s) that gets created on your destination target connection database for each of the schemas you load in this connection. So if your database has a schema named 'dbo' the target connection when synced will have a schema in that target database named the value of this field + '\_dbo'.
     * Alphanumeric characters only. It must start and end with a letter but can contain an underscore(\_).
   * Enter in the _**Server/Host**_ field, the name of the public server name or the IP Address (most customers use the IP for this field)
   * Enter in the **Port** field, where this database is accessible and the firewall restrictions are open
   * Enter in the **Database** field, the name of the database to connect
   * Enter in the _**Userame/Alias**_ field, the username of user you created in the steps above to give access to DataLakeHouse.io
   * Leave **Auth Type** field alone. It is set to password because DataLakeHouse is using TLS and requires username and password credentials to access the database
   * Enter in the **Password** field, the password for the user you created in the steps above
4. **Click Save & Test**
   * This attempt to connect to your database with the credentials provided.
   * A message of success or failure will be shown
     * If success you'll be prompted with the schema objects objects of the database and will need to complete the final steps for configuration shown below.
     * If failure happens with the test connection, the connection is still saved but you will need to correct the failure based on the failure reason information provided in the message.

### Instructions (Continued & Final Setup)

This section of steps ensures you have coverage of other important steps required on your database side and in DataLakeHouse.io once you have completed the above test connection successfully.

#### **Enable Change Tracking or Change Data Capture**

* To capture incremental loads of the database records being synchronized and to reduce cost we use this native feature of SQL Server through Change Tracking (CT) or Change Data Capture (CDC).  You could enable both if that is your desire but most companies set up one or the other based on the needs/content of the table.  You must set up at least one of these on each table that you require to be synchronized.
* Determine which you will use and on which tables.&#x20;
  * Use CDC: typically if you want to capture incremental changes when you are synchronizing data incrementally through the day (or more inline with the frequency of data change). We recommend that you do not use the net changes option when setting up CDC on your tables using the MS SQL Server commands.
  * Use Change Tracking (CT): typically when you just care about the change that happens in general during the sync frequency, or said another way, just getting the change at the end of the day.

#### Ensure Setup of Allow TCP/IP Protocol is Enabled

Remember DataLakeHouse.io connects to your database instance with credentials supplied by you. We store your credentials securely with our bank-grade protocols. DataLakeHouse.io will connect through SSH Tunnel TCP/IP or via standard internet traffic. You must have enabled SQL Server configuration to provide access to your SQL Server database(s), and ensure that you have [whitelisted/grantlisted our DataLakeHouse.io IP addresses](https://datalakehouse.io/whitelist-ip-addresses) that will access your SQL Server database(s).

To verify or setup port configuration on your instance via the SQL Server Configuration, follow these instructions:

1. On a standard managed SQL Server machine, access your SQL Server Configuration Manager and access the SQL Server Network Configuration.
2. Expand and access Protocols for , usually "Protocols for MSSQLSERVER"
3. Ensure that TCP/P is with an ENABLED status. (If it is disabled, right-click and select Enable.)
4. Confirm the port and the IP address by right clicking on TCP/IP > Properties
5. Click on the IP Addresses tab and scroll down to the IPAll section
6. Confirm the IP address which is usually 1433. Enter the IP Address of 1433 if not previously entered already.
7. Click the "Apply" button, then click the "OK" button on the prompt.
8. Return to the main area of the SQL Server Configuration Manager and expand SQL Native Client XX.X Configuration
9. Click on the Client Protocols option then in the right side ensure the TCP/IP status is set to Enabled.
10. Right-click on the TCP/IP row and verify the Default Port settings. This is typically 1433, but confirm the port or enter 1433, then click the "Apply" button
11. Return to the main area of the SQL Server Configuration Manager, and in the left side find, one of the top options, "SQL Server Services".
12. Right-click on "SQL Server Services", then click the "Restart" option. This will confirm all the above especially if any settings were modified. The restart should be complete under 90 seconds typically.

Reference for the above from [Microsoft SQL Server documentation](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port?view=sql-server-ver15)
