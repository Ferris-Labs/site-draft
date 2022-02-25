---
title: "Database Integration"
linkTitle: "Database Integration"
weight: -10
description: >-
  How to integrate a Database with the Ferris Platform.
---
## Install Database Drivers

Ferris DX requires a Python DB-API database driver and a SQLAlchemy dialect to be installed for each datastore you want to connect to within the executor image.

The following table provides a guide on the python libs to be installed.

You can read more here about how to install new database drivers and libraries into your FerrisDX executor image.

A list of some of the recommended packages.

| Database                                                     | PyPI package                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Amazon Athena](https://superset.apache.org/docs/databases/athena) | `pip install "PyAthenaJDBC>1.0.9` , `pip install "PyAthena>1.2.0` |
| [Amazon Redshift](https://superset.apache.org/docs/databases/redshift) | `pip install sqlalchemy-redshift`                            |
| [Apache Drill](https://superset.apache.org/docs/databases/drill) | `pip install sqlalchemy-drill`                               |
| [Apache Druid](https://superset.apache.org/docs/databases/druid) | `pip install pydruid`                                        |
| [Apache Hive](https://superset.apache.org/docs/databases/hive) | `pip install pyhive`                                         |
| [Apache Impala](https://superset.apache.org/docs/databases/impala) | `pip install impyla`                                         |
| [Apache Kylin](https://superset.apache.org/docs/databases/kylin) | `pip install kylinpy`                                        |
| [Apache Pinot](https://superset.apache.org/docs/databases/pinot) | `pip install pinotdb`                                        |
| [Apache Solr](https://superset.apache.org/docs/databases/solr) | `pip install sqlalchemy-solr`                                |
| [Apache Spark SQL](https://superset.apache.org/docs/databases/spark-sql) | `pip install pyhive`                                         |
| [Ascend.io](https://superset.apache.org/docs/databases/ascend) | `pip install impyla`                                         |
| [Azure MS SQL](https://superset.apache.org/docs/databases/sql-server) | `pip install pymssql`                                        |
| [Big Query](https://superset.apache.org/docs/databases/bigquery) | `pip install pybigquery`                                     |
| [ClickHouse](https://superset.apache.org/docs/databases/clickhouse) | `pip install clickhouse-driver==0.2.0 && pip install clickhouse-sqlalchemy==0.1.6` |
| [CockroachDB](https://superset.apache.org/docs/databases/cockroachdb) | `pip install cockroachdb`                                    |
| [Dremio](https://superset.apache.org/docs/databases/dremio)  | `pip install sqlalchemy_dremio`                              |
| [Elasticsearch](https://superset.apache.org/docs/databases/elasticsearch) | `pip install elasticsearch-dbapi`                            |
| [Exasol](https://superset.apache.org/docs/databases/exasol)  | `pip install sqlalchemy-exasol`                              |
| [Google Sheets](https://superset.apache.org/docs/databases/google-sheets) | `pip install shillelagh[gsheetsapi]`                         |
| [Firebolt](https://superset.apache.org/docs/databases/firebolt) | `pip install firebolt-sqlalchemy`                            |
| [Hologres](https://superset.apache.org/docs/databases/hologres) | `pip install psycopg2`                                       |
| [IBM Db2](https://superset.apache.org/docs/databases/ibm-db2) | `pip install ibm_db_sa`                                      |
| [IBM Netezza Performance Server](https://superset.apache.org/docs/databases/netezza) | `pip install nzalchemy`                                      |
| [MySQL](https://superset.apache.org/docs/databases/mysql)    | `pip install mysqlclient`                                    |
| [Oracle](https://superset.apache.org/docs/databases/oracle)  | `pip install cx_Oracle`                                      |
| [PostgreSQL](https://superset.apache.org/docs/databases/postgres) | `pip install psycopg2`                                       |
| [Trino](https://superset.apache.org/docs/databases/trino)    | `pip install sqlalchemy-trino`                               |
| [Presto](https://superset.apache.org/docs/databases/presto)  | `pip install pyhive`                                         |
| [SAP Hana](https://superset.apache.org/docs/databases/hana)  | `pip install hdbcli sqlalchemy-hana or pip install apache-superset[hana]` |
| [Snowflake](https://superset.apache.org/docs/databases/snowflake) | `pip install snowflake-sqlalchemy`                           |
| SQLite                                                       | No additional library needed                                 |
| [SQL Server](https://superset.apache.org/docs/databases/sql-server) | `pip install pymssql`                                        |
| [Teradata](https://superset.apache.org/docs/databases/teradata) | `pip install teradatasqlalchemy`                             |
| [Vertica](https://superset.apache.org/docs/databases/vertica) | `pip install sqlalchemy-vertica-python`                      |
| [Yugabyte](https://superset.apache.org/docs/databases/yugabyte) | `pip install psycopg2`                                       |

------

Note that many other databases are supported, the main criteria being the existence of a functional SQLAlchemy dialect and Python driver. Searching for the keyword "sqlalchemy + (database name)" should help get you to the right place.

If your database or data engine isn't on the list but a SQL interface exists, please file an issue so we can work on documenting and supporting it.