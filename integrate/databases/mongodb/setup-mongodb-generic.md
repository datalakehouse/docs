# Add a Generic MongoDB Data Source

Connect a Mongo DB database (Replica Set)
-----------------------------------------

Go ahead and gather the basic details:

* Database host or IP Address of the SRV host record
* Database port # (default is 27017) - 27017 is the fixed port we use to connect to your server (ask support if needing to change)

**MongoDB Specifications Required:**

* ReplicaSet or standalone instance of MongoDB
* Primary ReplicaSet Node Information
* MongoDB Version 3.1+ (talk w/ support if other versions needed)
* Determine which way to connect: TLS or SSH Tunneling
    * _As of July 2021 only the default SSL approach is available. This is just like if you were to connect from your MongoDB Shell, Compass, etc for example._
    * _MongoDB has some good [instructions on TLS setup](https://docs.mongodb.com/manual/core/security-transport-encryption/ "MongoDB instructions on TLS") which may be incorporated in a future release (contact support if you have urgent needs)_
* Firewalls on your database server should allow incoming connections through the public internet on your MongoDB port (typically 27017 unless your network guys have changed it).  Be sure to [Grantlist/Whitelist our DataLakeHouse.io IP addresses](https://www.datalakehouse.io/platform/grantlist-ip-addresses "DataLakeHouse IPs") for your database server network access.
    * For example, in MongoDB Atlas this is done by navigating in the left side panel Security > Network Access then clicking on the Add IP Addressess button.

Instructions (Basic Connection Setup)
-------------------------------------

Scroll down to ensure you review all steps, as needed...

Remember DataLakeHouse.io connects to your database instance with credentials supplied by you. We store your credentials securely with our bank-grade protocols.

1.  **Create a DataLakeHouse user on the MongoDB server (Atlas or Shell)**
    * If using MongoDB Atlas:
        * Log into MongoDB Atlas
        * Click on your respective Organization and select the Project
        * In the left menu under Security click Database Access
        * Click Add New Database user
        * Choose 'Password' as the Authentication Method
        * Enter a password that aligns with your policies and store it in a safe place for your reference in the subsequent connection steps
        * Under Database User Privileges, select the option 'Grant sepcific privileges', then the Specific Privileges area will appear
        * Under Specific Privileges you will need to have two privilege rows configured when finished, so select the first role from the dropdown as 'readAnyDatabase', then click the '+ Add another role' and select the 'read' option and in this new row enter the term 'local in the Database field; leaving the Collection field blank
        * Click the Add User button in the bottom right of the form.
    * If using MongoDB shell:
        * Connect to the MongoDB server with your admin user.
        * Create a user for DataLakeHouse using the following shell logic replacing the logic below for user and pwd &lt;password&gt; and choose a good password that complies with your security policies. We recommend the user name 'datalakehouse\_sync\_reader' but be sure to align with your policies.
            
                use admin
                db.createUser({
                    user: 'datalakehouse_sync_reader',
                    pwd: '<password>',
                    roles: [ 'readAnyDatabase', {role: 'read', db: 'local'} ]
                })
            
2.  **OpLog Size & Change Streams Configurations**
    * We use both [OpLog](https://docs.mongodb.com/v5.0/reference/glossary/#std-term-oplog) and [Change Streams](https://docs.mongodb.com/v5.0/changeStreams/) to sync your data and we recommend at least 48 hours sizing of the oplog for data retention. But we highly recommend setting oplog sizing to retain 5-7 days worth of data.  You can set the size for the oplog by following the steps:
        * [Change the oplog size for Replica Set](https://docs.mongodb.com/manual/tutorial/change-oplog-size/)
        * MongoDB Atlas : [Change the oplog size of the Cluster](https://docs.atlas.mongodb.com/cluster-config/additional-options/#set-oplog-size)
    * Contact support if you are unsure of how to set the oplog size.
3.  **On the Connection Form :: Enter your Credentials and Other Information**
    * Enter in the _**Name/Alias**_ field, the name you'll use within datalakehouse.io to differentiate this connection from others
    * Enter in the _**Target Schema Prefix**_ field, is the prefix of schema(s) that gets created on your destination target connection database for each of the schemas you load in this connection. So if your database has a schema named 'dbo' the target connection when synced will have a schema in that target database named the value of this field + '_dbo'.
        * Alphanumeric characters only. It must start and end with a letter but can contain an underscore(_).
            
    * Enter in the _**Server/Host**_ field, the name of the public server name or the IP Address (most customers use the IP for this field)
        * _if you have a mongodb+srv:// connection, enter the primary replica set with no port number, ex: mymongo-prod.mongodb.net_
        * _if you have a biconnector or mongodb:// connection, enter the main node with the port, ex: mymongo-prod-server.mongodb.net:27017_
    * Enter in the **Port** field, where this database is accessible and the firewall restrictions are open. For MongoDB we always assume port 27017.
    * Enter in the **Database** field, the name of the database to connect
    * Enter in the _**Userame/Alias**_ field, the username of user you created in the steps above to give access to DataLakeHouse.io
    * Leave **Auth Type** field alone. It is set to password because DataLakeHouse is using SSL/TLS and requires username and password credentials to access the database
    * Enter in the **Password** field, the password for the user you created in the steps above
    * Click on **Save & Test** to save the connection and test that we can connect.
4.  **If updating the form Click Save & Test or just Test**
    * Clicking on Save & Test will again save any changes such as the password change, etc.  You will not be able to change the prefix of the schema that will be the target in the destination. Any test of the connection will attempt to connect to your database with the credentials and info provided.
    * A message of success or failure will be shown:
        * If success you'll be prompted with the schema objects objects of the database and will need to complete the final steps for configuration shown below.
        * If failure happens with the test connection, the connection is still saved but you will need to correct the failure based on the failure reason information provided in the message

Other Information About This Connection
---------------------------------------

From time to time we will update the instruction set here to inform you about this connection or how specifically we must connect to optimally synchronize your data.

There is also great article here or SRV connection strings, [https://www.mongodb.com/developer/article/srv-connection-strings/](https://www.mongodb.com/developer/article/srv-connection-strings/)