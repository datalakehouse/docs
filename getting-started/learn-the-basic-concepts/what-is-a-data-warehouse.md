---
description: >-
  A single-source-of-truth (SSOT) is mandatory for a true data-driven
  organization! 'Nuff Said!
---

# What is a Data Warehouse?

All true business analysts or executive management leadership that has worked effectively with data in the last two decades understands that a centralized data repository, often known as a Data Warehouse or a Data Vault, is an absolute must.&#x20;

A **data warehouse** is a central repository of information that is designed for analytical rather than transactional work in order to make more informed decisions. It collects and aggregates data from one or many sources so it can be analyzed to produce business insights. It serves as a federated repository for all or certain data sets collected by a business’s operational systems.

Business analysts, data engineers, data scientists, and decision makers access the data through business intelligence (BI) tools, SQL clients, and other analytics applications.

Data and analytics have become indispensable to businesses to stay competitive. Business users rely on reports, dashboards, and analytics tools to extract insights from their data, monitor business performance, and support decision making. Data warehouses power these reports, dashboards, and analytics tools by storing data efficiently to minimize the input and output (I/O) of data and deliver query results quickly to hundreds and thousands of users concurrently.

## DATA WAREHOUSE VS. DATABASE

A data warehouse focuses on collecting data from multiple sources to facilitate broad access and analysis. They specialize in data aggregation and providing a longer view of an organization’s data over time.  A data warehouse is optimized to store large volumes of historical data and enables fast and complex querying of that data. Standard operational databases focus on transactional functions such as real-time data updates for ongoing business processes.

### WHAT IS DATA WAREHOUSING USED FOR?

Data warehousing has two key functions. First, it serves as a historical repository for integrating the information and data that is needed by the business, which may come from a variety of different sources. Second, it serves as a query execution and processing engine for that data, enabling end users to interact with the data that is stored in the database.

Complex queries are very difficult to run without a temporary pause of database update operations. A frequently paused transactional database will inevitably lead to data errors and gaps. Therefore a data warehouse serves as a separate platform for aggregation across multiple sources and then for analytics tasks across those diverse sources. This separation of roles allows databases to remain focused on purely transactional jobs without interruption.

A data warehouse is usually a [relational database](https://en.wikipedia.org/wiki/Relational\_database), traditionally housed on an enterprise server. Today, cloud-built and hybrid cloud data warehouses are becoming more common and popular. Pure cloud data warehousing allows businesses to easily scale compute resources up, down, or even out to handle increased volume and concurrency demands. It also allows organizations to easily facilitate data sharing without having to move data via ETL or other means.  The more sophisticated cloud data warehouses can also easily ingest and aggregate both semi-structured data (such as JSON) and structured data in unified relational SQL views. This allows businesses in the age of mobile and IoT to analyze and share disparate data sources with minimum effort, speeding time to insight.
