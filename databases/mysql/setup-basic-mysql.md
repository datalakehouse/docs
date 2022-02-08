<div id='dlh-instructions-body' class='dlh-instructions-body'>
  <h2>Let's connect your MySQL database!</h2>
  <p>Go ahead and gather the basic details:</p>
  <ul>
  <li>Database host or IP Address</li>
  <li>Database port # (default is 3306)</li>
  <li><span style='background-color: #fbeeb8;'>Replica ID for DataLakeHouse.io</span>
  <ul>
  <li>We connect to the MySQL datbase as a replica and thefore need to use this unique id to avoid conflicts with your existing replica IDs. The number will be a number greater than 100000 so this should eliminate any replica id conflict concerns.</li>
  </ul>
  </li>
  </ul>
  <p><strong>MySQL Specifications Required:</strong></p>
  <ul>
  <li>All recent and LTS versions (5.5 or above) are supported</li>
  <li>Determine which way to connect: TLS or SSH Tunneling</li>
  <li>Firewalls on your database server should allow incoming connections through the public internet on your MySQL port (typically 3306 unless your network team has changed it). &nbsp; <span style='background-color: #fbeeb8;'>Be sure to <a title='DataLakeHouse IPs' href='https://datalakehouse.io/whitelist-ip-addresses' target='_blank' rel='noopener'>whitelist our DataLakeHouse.io IP addresses</a> for your database server network access.</span></li>
  <li><span style='background-color: #fbeeb8;'>Be cognizant of using binlog_row_metadata settings for MySQL v8+, using a value of MINIMAL to prevent any sync issues.</span></li>
  </ul>
  <h2>Instructions (Basic Connection Setup)</h2>
  <pre class='editor-pre' data-copy-state='copy'>Scroll down to ensure you review all steps, as needed...</pre>
  <p>Remember DataLakeHouse.io connects to your database instance with credentials supplied by you. We store your credentials securely with our bank-grade protocols.</p>
  <ol style='list-style-type: upper-alpha;'>
  <li><strong>Create a DataLakeHouse user on the MySQL database</strong>
  <ul style='list-style-type: circle;'>
  <li>Connect to the MySQL database in question with your admin user.</li>
  <li>Create a user for DataLakeHouse using the following MySQL logic replacing &lt;newsername&gt; with you a user name that you choose (we recommend 'datalakehouse_ro' to signify a read-only user), and choose a good password that complies with your security policies:
  <pre class='editor-pre  language-sql'><code>
  CREATE USER &lt;new_username&gt;@'%' IDENTIFIED WITH mysql_native_password BY 'tmp!password';
  GRANT SELECT, REPLICATION CLIENT, REPLICATION SLAVE ON *.* TO &lt;new_username&gt;@'%';
  </code></pre>
  </li>
  </ul>
  </li>
  <li><strong>Enter your Credentials and Other Information in the Fields&nbsp;</strong>
  <ul style='list-style-type: circle;'>
  <li>Enter in the <em><strong>Name/Alias</strong></em> field, the name you'll use within datalakehouse.io to differentiate this connection from others</li>
  <li>Enter in the <em><strong>Target Schema Prefix</strong></em> field, is the prefix of schema(s) that gets created on your destination target connection database for each of the schemas you load in this connection. So if your database has a schema named 'dbo' the target connection when synced will have a schema in that target database named the value of this field + '_dbo'.
  <ul style='list-style-type: circle;'>
  <li>
  <div>
  <div>Alphanumeric characters only. It must start and end with a letter but can contain an underscore(_).</div>
  </div>
  </li>
  </ul>
  </li>
  <li>Enter in the <em><strong>Server/Host</strong></em> field, the name of the public server name or the IP Address (most customers use the IP for this field)</li>
  <li>Enter in the <strong>Port</strong> field, where this database is accessible and the firewall restrictions are open</li>
  <li>Enter in the <strong>Database</strong> field, the name of the database to connect</li>
  <li>Enter in the <em><strong>Userame/Alias</strong></em> field, the username of user you created in the steps above to give access to DataLakeHouse.io</li>
  <li>Leave <strong>Auth Type</strong> field alone. It is set to password because DataLakeHouse is using TLS and requires username and password credentials to access the database</li>
  <li>Enter in the <strong>Password</strong> field, the password for the user you created in the steps above</li>
  <li>&nbsp;</li>
  </ul>
  </li>
  <li><strong>Click Save &amp; Test</strong>
  <ul style='list-style-type: circle;'>
  <li>This attempt to connect to your database with the credentials provided.</li>
  <li>A message of success or failure will be shown
  <ul style='list-style-type: circle;'>
  <li>If success you'll be prompted with the schema objects objects of the database and will need to complete the final steps for configuration shown below.</li>
  <li>If failure happens with the test connection, the connection is still saved but you will need to correct the failure based on the failure reason information provided in the message</li>
  </ul>
  </li>
  </ul>
  </li>
  <li><strong>...</strong></li>
  </ol>
  <p>&nbsp;</p>
  <h2>Instructions (Continued &amp; Final Setup)</h2>
  <p>This section of steps ensures you have coverage of other important steps required on your database side and in DataLakeHouse.io once you have completed the above test connection successfully.</p>
  <h3><strong>Enable Change Tracking and BinLog</strong></h3>
  <ul style='list-style-type: circle;'>
  <li>To capture incremental loading delta changes of the database records being synchronized and to reduce cost we use this native feature of MySQL.&nbsp;&nbsp;</li>
  <li>Connect to your MySQL database server and access the file system</li>
  <li>Access the MySQL configuration file (Ex: /etc/my.cnf)
  <ul style='list-style-type: circle;'>
  <li>For more instructions follow the MySQL binlog setup process from the MySQL documentation</li>
  </ul>
  </li>
  <li>Make sure the file has the lines as follows in the [mysqld] section to enable ROW formatting binary log replication:
  <div>
  <pre class='editor-pre  language-bash'><code>
  [mysqld]
  binlog-format=ROW
  log-bin=mysql-binlog
  server-id=0000012345
  expire-logs-days=1
  log-slave-updates=1
  </code></pre>
  </div>
  <br />
  <ul style='list-style-type: circle;'>
  <li>Name the binary log, log-bin attribute, mysql-binlog</li>
  <li>Make sure a server-id exists with any number between 1 and 4000000000</li>
  <li>Make sure the expire-logs-days to 5, the minimum is one and most customers have a maximum of 7</li>
  </ul>
  </li>
  <li>Restart your MySQL server in order for the changes to propagate</li>
  <li><span style='background-color: #fbeeb8;'>Determine that your binlog is configured correctly,</span>&nbsp;</li>
  </ul>
  <p>&nbsp;</p>
  <h2>Other Information About This Connection</h2>
  <p>From time to time we will update the instruction set here to inform you about this connection or how specifically we must connect to optimally synchronize your data.</p>
  <p>If you require any other type of authorization to connect to your account instance please reach out to our support team via our <a href='https://datalakehouse.zendesk.com' target='_blank' rel='noopener'>DataLakeHouse Support Portal</a>.</p>
  </div>