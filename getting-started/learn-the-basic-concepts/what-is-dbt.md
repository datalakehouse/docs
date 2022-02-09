# What is dbt?

[dbt](https://www.getdbt.com) (data build tool) is a command line tool that enables data analysts and engineers to transform data in their warehouses more effectively.

**dbt is the T in** [**ELT**](what-is-elt.md)**.** It doesn’t extract or load data, but it’s extremely good at transforming data that’s already loaded into your warehouse. This “transform after load” architecture is becoming known as [ELT](what-is-elt.md) (extract, load, transform).

ELT has become commonplace because of the power of modern analytic databases. Data warehouses like Snowflake are extremely performant _and_ very scalable such that at this point most data transformation use cases can be much more effectively handled in-database rather than in some external processing layer. Add to this the separation of compute and storage and there are decreasingly few reasons to want to execute your data transformation jobs elsewhere.

**dbt’s only function is to take code, compile it to SQL, and then run against your database**. If you are comfortable with writing SQL you will be comfortable building with dbt. dbt makes it a breeze to write SQL-based data transformation logic against a data cloud.

DataLakeHouse leverages dbt for transformations within Snowflake and we absolutely love the tool! If you decide to extend the dbt models yourself you too will see how powerful and easy dbt is to use.

dbt is key to building a [Data Vault](https://patrickcuba.medium.com/data-vault-pitch-904511875b34) allowing you to quickly pivot as your organization changes without a large data warehouse project.&#x20;

![Image depicts where dbt fits into the data stack:](https://hackmd.io/\_uploads/BJqZomekc.png)
