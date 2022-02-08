# Add a Generic PostgreSQL Data Source

Let's connect your PostgreSQL database!
---------------------------------------

Go ahead and gather the basic details:

* Database host or IP Address
* Database port # (default is 3306)

**PostgreSQL Specifications Required:**

* All recent and LTS versions (5.5 or above) are supported
* Determine which way to connect: TLS or SSH Tunneling
* Firewalls on your database server should allow incoming connections through the public internet on your PostgreSQL port (typically 3306 unless your network team has changed it).   Be sure to [whitelist our DataLakeHouse.io IP addresses](https://datalakehouse.io/whitelist-ip-addresses "DataLakeHouse IPs") for your database server network access.
* Be cognizant of using binlog\_row\_metadata settings for PostgreSQL v8+, using a value of MINIMAL to prevent any sync issues.

Instructions (Basic Connection Setup)
-------------------------------------

Scroll down to ensure you review all steps, as needed...

Remember DataLakeHouse.io connects to your database instance with credentials supplied by you. We store your credentials securely with our bank-grade protocols.

1.  **Create a DataLakeHouse user on the PostgreSQL database**
    * Connect to the PostgreSQL database in question with your admin user.
    * Create a user for DataLakeHouse using the following PostgreSQL logic replacing &lt;newsername&gt; with you a user name that you choose (we recommend 'datalakehouse_ro' to signify a read-only user), and choose a good password that complies with your security policies:
        
            
              CREATE USER <new_username>@'%' IDENTIFIED WITH PostgreSQL_native_password BY 'tmp!password';
              GRANT SELECT, REPLICATION CLIENT, REPLICATION SLAVE ON *.* TO <new_username>@'%';
              
        
2.  **Enter your Credentials and Other Information in the Fields **
    * Enter in the _**Name/Alias**_ field, the name you'll use within datalakehouse.io to differentiate this connection from others
    * Enter in the _**Target Schema Prefix**_ field, is the prefix of schema(s) that gets created on your destination target connection database for each of the schemas you load in this connection. So if your database has a schema named 'dbo' the target connection when synced will have a schema in that target database named the value of this field + '_dbo'.
        * Alphanumeric characters only. It must start and end with a letter but can contain an underscore(_).
            
    * Enter in the _**Server/Host**_ field, the name of the public server name or the IP Address (most customers use the IP for this field)
    * Enter in the **Port** field, where this database is accessible and the firewall restrictions are open
    * Enter in the **Database** field, the name of the database to connect
    * Enter in the _**Userame/Alias**_ field, the username of user you created in the steps above to give access to DataLakeHouse.io
    * Leave **Auth Type** field alone. It is set to password because DataLakeHouse is using TLS and requires username and password credentials to access the database
    * Enter in the **Password** field, the password for the user you created in the steps above
    
3.  **Click Save & Test**
    * This attempt to connect to your database with the credentials provided.
    * A message of success or failure will be shown
        * If success you'll be prompted with the schema objects objects of the database and will need to complete the final steps for configuration shown below.
        * If failure happens with the test connection, the connection is still saved but you will need to correct the failure based on the failure reason information provided in the message
4.  **...**

Instructions (Continued & Final Setup)
--------------------------------------

This section of steps ensures you have coverage of other important steps required on your database side and in DataLakeHouse.io once you have completed the above test connection successfully.

### **Enable Change Tracking and BinLog**

* To capture incremental loading delta changes of the database records being synchronized and to reduce cost we use this native feature of PostgreSQL.  
* Connect to your PostgreSQL database server and access the file system
* Access the PostgreSQL configuration file (Ex: /etc/my.cnf)
    * For more instructions follow the PostgreSQL binlog setup process from the PostgreSQL documentation
* Make sure the file has the lines as follows in the \[PostgreSQLd\] section to enable ROW formatting binary log replication:
    
        
          [PostgreSQLd]
          binlog-format=ROW
          log-bin=PostgreSQL-binlog
          server-id=0000012345
          expire-logs-days=1
          log-slave-updates=1
          
    
      
    * Name the binary log, log-bin attribute, PostgreSQL-binlog
    * Make sure a server-id exists with any number between 1 and 4000000000
    * Make sure the expire-logs-days to 5, the minimum is one and most customers have a maximum of 7
* Restart your PostgreSQL server in order for the changes to propagate
* Determine that your binlog is configured correctly, 

Other Information About This Connection
---------------------------------------

From time to time we will update the instruction set here to inform you about this connection or how specifically we must connect to optimally synchronize your data.

If you require any other type of authorization to connect to your account instance please reach out to our support team via our [DataLakeHouse Support Portal](https://datalakehouse.zendesk.com).