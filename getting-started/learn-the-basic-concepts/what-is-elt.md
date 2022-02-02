---
description: Extract Load Transform
---

# What is ELT?

The move from building ETL pipelines (where much of the transformation is carried out in tools like Spark or Informatica before the data is loaded into Snowflake) to ELT pipelines (where the transformation is carried out within Snowflake itself). The reasons are that (1) SQL is easier for business users to write (2) Snowflake scales better and is less expensive than alternative data processing technologies.

The problem with doing all the transformation code in SQL, though, is that it can become hard to maintain. How often have you come back to a project after a few months and been faced with a bunch of views, tables, user-defined functions, and scripts and scratched your head in confusion?

That’s why it’s very useful to have a environment that supports best practices in terms of transformation code — the same sort of best practices you want to apply to any code: documentation, reusability, readability, assertions, unit testing, source code control, and so on.

* [dbt](what-is-dbt.md) and [DataForm](what-is-dataform.md) are our main tools for incorporating ELT within DataLakeHouse forming the modern data stack engine

ELT brings a software engineering approach to data modeling and pipelines making data transformations more accessible and reliable:

1. **Collaborate and create data pipelines**—Develop data workflows in SQL and collaborate with others via Git. Include data documentation that is automatically visible to others.
2. **Deploy data pipelines**—Keep logical data up-to-date by scheduling data workflows which incrementally update downstream datasets, reducing cost and latency.
3. **Ensure data quality**—Define data quality checks in SQL and automatically receive alerts when those checks fail. View logs, version history and dependency graphs to understand changes in data.
