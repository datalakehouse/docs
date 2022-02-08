<div id='dlh-instructions-body' class='dlh-instructions-body'>
<h2>Connect a Mongo DB database (Replica Set)</h2>
<p>Go ahead and gather the basic details:</p>
<ul>
<li>Database host or IP Address of the SRV host record</li>
<li>Database port # (default is 27017) - <span style='background-color: #fbeeb8;'>27017 is the fixed port we use to connect </span>to your server (ask support if needing to change)</li>
</ul>
<p><strong>MongoDB Specifications Required:</strong></p>
<ul>
<li>ReplicaSet or standalone instance of MongoDB</li>
<li>Primary ReplicaSet Node Information</li>
<li>MongoDB Version 3.1+ (talk w/ support if other versions needed)</li>
<li>Determine which way to connect: TLS or SSH Tunneling
<ul>
<li><em>As of July 2021 <span style='text-decoration: underline;'>only</span> the default SSL approach is available. This is just like if you were to connect from your MongoDB Shell, Compass, etc for example.</em></li>
<li><em>MongoDB has some good <a title='MongoDB instructions on TLS' href='https://docs.mongodb.com/manual/core/security-transport-encryption/' target='_blank' rel='noopener'>instructions on TLS setup</a> which may be incorporated in a future release (contact support if you have urgent needs)</em></li>
</ul>
</li>
<li>Firewalls on your database server should allow incoming connections through the public internet on your MongoDB port (typically 27017 unless your network guys have changed it).&nbsp; <span style='background-color: #fbeeb8;'>Be sure to <a title='DataLakeHouse IPs' href='https://www.datalakehouse.io/platform/grantlist-ip-addresses' target='_blank' rel='noopener'>Grantlist/Whitelist our DataLakeHouse.io IP addresses</a> for your database server network access.</span>
<ul>
<li><span style='background-color: #fbeeb8;'>For example, in MongoDB Atlas this is done by navigating in the left side panel Security &gt; Network Access then clicking on the Add IP Addressess button.</span></li>
</ul>
</li>
</ul>
<h2>Instructions (Basic Connection Setup)</h2>
<pre class='editor-pre' data-copy-state='copy'>Scroll down to ensure you review all steps, as needed...</pre>
<p>Remember DataLakeHouse.io connects to your database instance with credentials supplied by you. We store your credentials securely with our bank-grade protocols.</p>
<ol style='list-style-type: upper-alpha;'>
<li><strong>Create a DataLakeHouse user on the MongoDB server (Atlas or Shell)</strong>
<ul style='list-style-type: circle;'>
<li>If using MongoDB Atlas:
<ul>
<li>Log into MongoDB Atlas</li>
<li>Click on your respective Organization and select the Project</li>
<li>In the left menu under Security click Database Access</li>
<li>Click Add New Database user</li>
<li>Choose 'Password' as the Authentication Method</li>
<li>Enter a password that aligns with your policies and store it in a safe place for your reference in the subsequent connection steps</li>
<li>Under Database User Privileges, select the option 'Grant sepcific privileges', then the Specific Privileges area will appear</li>
<li>Under Specific Privileges you will need to have two privilege rows configured when finished, so select the first role from the dropdown as 'readAnyDatabase', then click the '+ Add another role' and select the 'read' option and in this new row enter the term 'local in the Database field; leaving the Collection field blank</li>
<li>Click the Add User button in the bottom right of the form.</li>
</ul>
</li>
<li>If using MongoDB shell:
<ul style='list-style-type: circle;'>
<li>Connect to the MongoDB server with your admin user.</li>
<li>Create a user for DataLakeHouse using the following shell logic replacing the logic below for user and pwd &lt;password&gt; and choose a good password that complies with your security policies. We recommend the user name 'datalakehouse_sync_reader' but be sure to align with your policies.
<pre class='language-sql'><code>use admin
db.createUser({
    user: 'datalakehouse_sync_reader',
    pwd: '&lt;password&gt;',
    roles: [ 'readAnyDatabase', {role: 'read', db: 'local'} ]
})</code></pre>
</li>
</ul>
</li>
</ul>
</li>
<li><strong>OpLog Size &amp; Change Streams Configurations</strong>
<ul style='list-style-type: circle;'>
<li>We use both <a href='https://docs.mongodb.com/v5.0/reference/glossary/#std-term-oplog' target='_blank' rel='noopener'>OpLog</a> and <a href='https://docs.mongodb.com/v5.0/changeStreams/' target='_blank' rel='noopener'>Change Streams</a> to sync your data and we recommend at least 48 hours sizing of the oplog for data retention. But we highly recommend setting oplog sizing to retain 5-7 days worth of data.&nbsp; You can set the size for the oplog by following the steps:
<ul style='list-style-type: circle;'>
<li><a href='https://docs.mongodb.com/manual/tutorial/change-oplog-size/' target='_blank' rel='noopener'>Change the oplog size for Replica Set</a></li>
<li>MongoDB Atlas : <a href='https://docs.atlas.mongodb.com/cluster-config/additional-options/#set-oplog-size' target='_blank' rel='noopener'>Change the oplog size of the Cluster</a></li>
</ul>
</li>
<li>Contact support if you are unsure of how to set the oplog size.</li>
</ul>
</li>
<li><strong>On the Connection Form :: Enter your Credentials and Other Information</strong>
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
<li>Enter in the <em><strong>Server/Host</strong></em> field, the name of the public server name or the IP Address (most customers use the IP for this field)
<ul style='list-style-type: circle;'>
<li><em>if you have a mongodb+srv:// connection, enter the primary replica set with no port number, ex: mymongo-prod.mongodb.net</em></li>
<li><em>if you have a biconnector or mongodb:// connection, enter the main node with the port, ex: mymongo-prod-server.mongodb.net:27017</em></li>
</ul>
</li>
<li>Enter in the <strong>Port</strong> field, where this database is accessible and the firewall restrictions are open. For MongoDB we always assume port 27017.</li>
<li>Enter in the <strong>Database</strong> field, the name of the database to connect</li>
<li>Enter in the <em><strong>Userame/Alias</strong></em> field, the username of user you created in the steps above to give access to DataLakeHouse.io</li>
<li>Leave <strong>Auth Type</strong> field alone. It is set to password because DataLakeHouse is using SSL/TLS and requires username and password credentials to access the database</li>
<li>Enter in the <strong>Password</strong> field, the password for the user you created in the steps above</li>
<li>Click on <strong>Save &amp; Test </strong>to save the connection and test that we can connect.</li>
</ul>
</li>
<li><strong>If updating the form Click Save &amp; Test or just Test</strong>
<ul style='list-style-type: circle;'>
<li>Clicking on Save &amp; Test will again save any changes such as the password change, etc.&nbsp; You will not be able to change the prefix of the schema that will be the target in the destination. Any test of the connection will attempt to connect to your database with the credentials and info provided.</li>
<li>A message of success or failure will be shown:
<ul style='list-style-type: circle;'>
<li>If success you'll be prompted with the schema objects objects of the database and will need to complete the final steps for configuration shown below.</li>
<li>If failure happens with the test connection, the connection is still saved but you will need to correct the failure based on the failure reason information provided in the message</li>
</ul>
</li>
</ul>
</li>
</ol>
<h2>Other Information About This Connection</h2>
<p>From time to time we will update the instruction set here to inform you about this connection or how specifically we must connect to optimally synchronize your data.</p>
<p>There is also great article here or SRV connection strings, <a href='https://www.mongodb.com/developer/article/srv-connection-strings/' target='_blank' rel='noopener'>https://www.mongodb.com/developer/article/srv-connection-strings/</a></p>
</div>