# QuickBooks

QuickBooks Online is a cloud solution for accounting developed and marketed by Intuit. DataLakeHouse supports only QuickBooks Online, it does not support the desktop version of QuickBooks.&#x20;

Import QuickBooks Online Accounts, Bills, Invoices, Customers, etc. directly to your Target. You can schedule your QuickBooks Online integration operations, via a Sync Bridge, to execute it automatically.

It allows you to create a copy of QuickBooks Online data in Snowflake and keep it up-to-date with little to no configuration efforts. You don’t even need to prepare the schema — DataLakeHouse will automatically create tables for your cloud data.

All you need is to specify the connections to QuickBooks Online and your Target and select data to replicate, and DataLakeHouse does the rest. It will copy the specified QuickBooks Online data to the Target and maintain this copy up-to-date automatically with incremental updates.

## Connecting via QuickBooks Online, you need to make sure that: <a href="#connecting-via-quickbooks-online-you-need-to-make-sure-that" id="connecting-via-quickbooks-online-you-need-to-make-sure-that"></a>

* You are an administrator or an owner of your QuickBooks Online account. If you are not, please contact your QuickBooks Online administrator.

### Instructions (Basic Connection Setup) <a href="#instructions-basic-connection-setup" id="instructions-basic-connection-setup"></a>

DataLakeHouse.io securely connects to your QuickBooks Online instance by redirecting you to the QuickBooks portal for you to sign-in via QuickBooks's login. DataLakeHouse.io does not capture or store your password/credentials.Using the form please complete the following basic steps:

1. Enter a Name or Alias for this connection that is unique in the 'Name/Alias' field.
   * This name is only visible in DataLakeHouse.io and should be descriptive enough for you and other users of DataLakeHouse to understand its name.
2.  Enter a unique target schema name in your Target (Snowflake data cloud destination) in the 'Target Schema Prefix' where you wish to land the data.

    * The name must be at least two characters in length and should be a meaningful name, i.e. 'QuickBooks' or 'QB'.

    &#x20;               ![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6UvbtabOn9K6wMSo1Xek%2Fuploads%2FPJFI34dYL4YrtNQTIRmv%2Fimage.png?alt=media\&token=13bea6ed-7853-4783-a98e-fee47beffef9)​
3. Click the 'Authorize Your Account' button which will transport the page to the QuickBooks Online login, where you will enter your QuickBooks account credentials. Once your credentials are accepted you will be automatically redirected back to the DataLakeHouse.io portal and you will see a successful connection of your Source.

&#x20;                   ![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6UvbtabOn9K6wMSo1Xek%2Fuploads%2FDvVHJdv5bTvKRjoKehaa%2FScreen%20Shot%202022-02-01%20at%208.15.02%20AM.png?alt=media\&token=61f383ca-bc36-42d5-b5a8-11331b15dcec)​

If any issues occur with the QuickBooks Online authorization occur, simply return to the sources page in DataLakeHouse.io, edit this source and click the 'Authorize Your Account' or 'Re-Authorize Your Account' button. If any issues persist please contact our support team via the [DataLakeHouse Support Portal](https://datalakehouse.zendesk.com).
