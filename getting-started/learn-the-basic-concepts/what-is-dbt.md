# What is dbt?

[dbt](https://www.getdbt.com) (data build tool) is a command line tool that enables data analysts and engineers to transform data in their warehouses more effectively.&#x20;

**dbt is the T in ELT.** It doesn’t extract or load data, but it’s extremely good at transforming data that’s already loaded into your warehouse. This “transform after load” architecture is becoming known as ELT (extract, load, transform).

ELT has become commonplace because of the power of modern analytic databases. Data warehouses like Snowflake are extremely performant _and_ very scalable such that at this point most data transformation use cases can be much more effectively handled in-database rather than in some external processing layer. Add to this the separation of compute and storage and there are decreasingly few reasons to want to execute your data transformation jobs elsewhere.

dbt is a tool to help you write and execute the data transformation jobs that run inside your warehouse. **dbt’s only function is to take code, compile it to SQL, and then run against your database.**

dbt is made up of Jinja, custom Jinja extensions, a compiler, a runner, and a package manager. Combine those elements together and you get a complete programming environment for your database. There is no better way to write SQL-based data transformation logic against a data warehouse today.

DataLakeHouse leverages dbt for transformations within Snowflake and we absolutely love tool!&#x20;
