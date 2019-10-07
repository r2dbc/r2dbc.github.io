---
layout: page
title: Drivers
permalink: /drivers/
---

# Service Provider Interface (SPI)

R2DBC defines an SPI all data store drivers must implement:

* [r2dbc-spi](https://github.com/r2dbc/r2dbc-spi) - set of interfaces defining the SPI for R2DBC.
* [r2dbc-spi-test](https://github.com/r2dbc/r2dbc-spi/tree/master/r2dbc-spi-test) - a **Technology Compatibility Kit (TCK)** contained within the SPI repository for verifying your driver's implementation.

One noticeable difference between R2DBC and JDBC is that JDBC is aimed at both driver writers as well as application developers. Drivers and applications operate on different levels, making this one-size-fits-all less than ideal.

R2DBC's SPI is deliberately designed to be as small as possible while still capturing critical features for ANY relational data store. This means that data store specific extensions are not targeted by the SPI.

And to ease implementation, a test interface, a veritable TCK, is provided to ensure you are fully operational.

# Existing Drivers

R2DBC drivers implements the SPI listed above. The ones currently supported include:

* [cloud-spanner-r2dbc](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc) - Driver for Google Cloud Spanner.
* [jasync-sql](https://github.com/jasync-sql/jasync-sql) - R2DBC wrapper for Java & Kotlin Async Database Driver for MySQL and PostgreSQL written in Kotlin.
* [r2dbc-h2](https://github.com/r2dbc/r2dbc-h2) - Native driver implemented for H2 as a test database.
* [r2dbc-postgres](https://github.com/r2dbc/r2dbc-postgresql) - Native driver implemented for PostgreSQL.
* [r2dbc-mssql](https://github.com/r2dbc/r2dbc-mssql) - Native driver implemented for Microsoft SQL Server.
* [r2dbc-mysql](https://github.com/mirromutth/r2dbc-mysql) - Native driver implemented for MySQL.

# Connection Pooling

The following connection pool implementations are available for R2DBC:

* [r2dbc-pool](https://github.com/r2dbc/r2dbc-pool) - Reactive connection pooling using Reactor Pool.

# Implementing a driver

R2DBC has a clearly defined **SPI** you must implement to host a solution for your data store. To build an implementation, add the following artifact to your build:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi**

The key interface all driver providers must implement is the [`Connection`](https://r2dbc.io/spec/0.8.0.RC2/api/io/r2dbc/spi/Connection.html) and a set of other interfaces.
Check out the specification for details on [R2DBC Driver Compliance](/spec/0.8.0.RC2/spec/html/#compliance).

There are other parts to implement, but this is the core.

# Technology Compatibility Kit (TCK)

R2DBC also has a suite of test cases to verify your support. Your data store implementation should import a test-scoped dependency on:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi-test**

To run all the tests that are expected, write an implementation of the TCK's `TestKit<T>` test.

See [r2dbc-postgresql's Example](https://github.com/r2dbc/r2dbc-postgresql/blob/master/src/test/java/io/r2dbc/postgresql/PostgresqlTestKit.java) to read the full source.
