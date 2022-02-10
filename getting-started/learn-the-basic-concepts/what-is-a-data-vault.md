# What is a Data Vault?

Data Vault is a method and architecture for delivering a Data Analytics Service to an enterprise supporting its Business Intelligence, Data Warehousing, Analytics and Data Science requirements. At the core it is a modern, agile way of designing and building efficient, effective Data Warehouses. DataLakeHouse leverages a Data Vault 2.0 construct in order to quickly incorporate new data sources, new analytical models and various groups of users; i.e. analytics, data scientists, etc.

Data Vault modeling makes no distinction between good and bad data ("bad" meaning not conforming to business rules). This is summarized in the statement that a data vault stores "a single version of the facts" (also expressed by Dan Linstedt, pioneer of Data Vault, as "all the data, all of the time") as opposed to the practice in other data warehouse methods of storing "a single version of the truth" where data that does not conform to the definitions is removed or "cleansed".

### Why is Data Vault so useful?

The Data Vault is designed specifically for organizations that need to run agile Data Warehouse projects where scalability, integration, development speed and business orientation are important. With enterprise scale in mind, it embraces and improves on the best of traditional Data Warehouse design.

The modeling method is designed to be resilient to change in the business environment where the data being stored is coming from, by explicitly separating structural information from descriptive attributes. Data Vault is designed to enable parallel loading as much as possible, so that very large implementations can scale out without the need for major redesign.

### Data Vault vs Data Vault 2.0

Originally Data Vault majored around the modeling technique and data loading processes for the Data Warehouse. Data Vault 2.0 expands the scope of the method to cover the full Data Warehouse solution. Features include a reference architecture, development and operational processes, agile project delivery, automation and continuous improvement. There is also a body of evolving best practice keeping pace with changing technology.

### Data Lake and Data Vaults

Data Lakes and Data Vaults address different parts of the Analytics requirements for an organization and they complement each other.  A combined architecture is an increasingly common architectural design pattern.

Data Lakes provide a persistent staging area capturing a superset of the data being fed to the Data Vault.  This allows Data Vault to focus on integrating the most useful data for the business and importantly allow data feeds to be replayed over again providing a safety valve for experimentation.

A Data Vault complements the Data Lake and is a solution for those organizations that need to integrate and add structure to the data held in their Data Lake.

### Data Vault and Star Schemas

Data Vault 2.0 has staging, vault and mart layers. Star schemas live in the mart layer, each star schema exposes a subset of the vault for a particular group of users. Typically, hubs and their satellites form dimensions, links and their satellites form facts. Additional features (such as bridging tables and PIT tables) can be used to virtualize these – enabling them to run as performant views.
