# HBase Vs Relational Databases

| HBase | Relational Database |
|-|-|
| Does not have a fixed schema (schema-less). Defines only column families. | Has a fixed schema which describes the structure of the tables. |
| Works well with structured and semi-structured data. | Works well with structured data. |
| It can have de-normalized/sparse data (missing or NA values). | Can store only normalized data. |
| Built for wide tables that can be scaled horizontally. | Built for thin tables that is hard to scale. |

*HBase* **does not support SQL scripting**; instead the equivalent is written in Java, employing similarity with a *MapReduce* application.

The *Apache Phoenix* project provides a SQL layer for HBase as well as JDBC driver that can be integrated with various analytics and business intelligence applications.

The *Apache Trafodion* projcect provides a SQL query engine with ODBC and JDBC drivers and distributed ACID transaction protection across multiple statements, tables and rows that use HBase as a storage engine.
