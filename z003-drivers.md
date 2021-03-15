---
layout: page
title: Drivers
permalink: /drivers/
---

# Service Provider Interface (SPI)

R2DBC defines an SPI all data store drivers must implement.

* [r2dbc-spi](https://github.com/r2dbc/r2dbc-spi): a set of interfaces defining the SPI for R2DBC.
* [r2dbc-spi-test](https://github.com/r2dbc/r2dbc-spi/tree/main/r2dbc-spi-test): within the SPI repository, a Technology Compatibility Kit (TCK) for verifying a driver's implementation.

One noticeable difference between R2DBC and JDBC is that JDBC is aimed at both driver writers and application developers. Driver developers and application developers operate at different levels, making this one-size-fits-all model less than ideal.

R2DBC's SPI is deliberately designed to be as small as possible, while still including features critical for _any_ relational data store. This means that the SPI does not target extensions which are specific to a data store.

To ease implementation, R2DBC also provides a test interface (a veritable TCK) to ensure your driver is fully operational.

# Driver Implementations

R2DBC drivers implement the SPI listed above. The ones currently supported include:

* [cloud-spanner-r2dbc](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc) - driver for Google Cloud Spanner.
* [jasync-sql](https://github.com/jasync-sql/jasync-sql) - R2DBC wrapper for Java & Kotlin Async Database Driver for MySQL and PostgreSQL (written in Kotlin).
* [oracle-r2dbc](https://github.com/oracle/oracle-r2dbc) - native driver implemented for Oracle.
* [r2dbc-h2](https://github.com/r2dbc/r2dbc-h2) - native driver implemented for H2 as a test database.
* [r2dbc-mariadb](https://github.com/mariadb-corporation/mariadb-connector-r2dbc) - native driver implemented for MariaDB.
* [r2dbc-mssql](https://github.com/r2dbc/r2dbc-mssql) - native driver implemented for Microsoft SQL Server.
* [r2dbc-mysql](https://github.com/mirromutth/r2dbc-mysql) - native driver implemented for MySQL.
* [r2dbc-postgres](https://github.com/r2dbc/r2dbc-postgresql) - native driver implemented for PostgreSQL.

# Connection Pooling

The following connection pool implementations are available for R2DBC:

* [r2dbc-pool](https://github.com/r2dbc/r2dbc-pool) - reactive connection pooling using Reactor Pool.

# Observability

Observability is provided through [`r2dbc-proxy`](https://github.com/r2dbc/r2dbc-proxy).

# Implementing a Driver

R2DBC has a clearly-defined SPI, which you must implement to host a solution for your data store. To build an implementation, add the following artifact to your build:

* **Group** `io.r2dbc`
* **Artifact** `r2dbc-spi`

The key interface that all driver providers must implement is the [`Connection`](https://r2dbc.io/spec/0.8.2.RELEASE/api/io/r2dbc/spi/Connection.html), along with a set of other interfaces.
Check out the specification for details on [R2DBC Driver Compliance](/spec/0.8.2.RELEASE/spec/html/#compliance).

There are other parts to implement, but this is the core.

# Technology Compatibility Kit (TCK)

R2DBC also has a suite of test cases to verify your driver's support. Your data store implementation should import a test-scoped dependency on the following artifact:

* **Group** `io.r2dbc`
* **Artifact** `r2dbc-spi-test`

To run all of the expected tests, write an implementation of the TCK's `TestKit<T>` test.

See the [example in r2dbc-postgresql](https://github.com/r2dbc/r2dbc-postgresql/blob/main/src/test/java/io/r2dbc/postgresql/PostgresqlTestKit.java) to read the full source.
