---
layout: default
---

The Reactive Relational Database Connectivity (R2DBC) project brings reactive programming APIs to relational databases.

# In a Nutshell

**Based on the Reactive Streams specification.** R2DBC is founded on the Reactive Streams specification, which provides a fully-reactive non-blocking API.

**Works with relational databases.** In contrast to the blocking nature of JDBC, R2DBC allows you to work with SQL databases using a reactive API.

**Supports scalable solutions.** With Reactive Streams, R2DBC enables you to move from the classic "one thread per connection" model to a more powerful and scalable approach.

**Provides an open specification.** R2DBC is an open specification and establishes a Service Provider Interface (SPI) for driver vendors to implement and clients to consume.

# Features

* Broad type conversion
* Transactions, isolation levels, and save points
* Batching
* BLOB/CLOB
* Connection URLs
* `ConnectionFactory` discovery and configuration based on Java's `ServiceLoader`
* Observability

## Latest Release

The latest release of R2DBC is 0.8.2.RELEASE. You can [download the spec](/spec/0.8.2.RELEASE/spec/html/) or [browse the Javadoc](/spec/0.8.2.RELEASE/api/).

## Driver Implementations

For more information, see the [Drivers](/drivers/) page.

* [cloud-spanner-r2dbc](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc): driver for Google Cloud Spanner
* [jasync-sql](https://github.com/jasync-sql/jasync-sql): R2DBC wrapper for Java & Kotlin Async Database Driver for MySQL and PostgreSQL written in Kotlin.
* [r2dbc-h2](https://github.com/r2dbc/r2dbc-h2): native driver implemented for H2 as a test database.
* [r2dbc-postgres](https://github.com/r2dbc/r2dbc-postgresql): native driver implemented for PostgreSQL.
* [r2dbc-mssql](https://github.com/r2dbc/r2dbc-mssql): native driver implemented for Microsoft SQL Server.
* [r2dbc-mysql](https://github.com/mirromutth/r2dbc-mysql): native driver implemented for MySQL.

## Connection Pooling

Connection pooling is provided through the reactive connection pool implementation in [`r2dbc-pool`](https://github.com/r2dbc/r2dbc-pool).

## Observability

Observability is provided through [`r2dbc-proxy`](https://github.com/r2dbc/r2dbc-proxy).

# Relational Meets Reactive

Existing standards, based on blocking I/O, cut off reactive programming from relational database users. R2DBC specifies a new API to allow reactive code that works efficiently with relational databases.

R2DBC is a specification designed from the ground up for reactive programming with SQL databases. It defines a non-blocking SPI for database driver implementors and client library authors. R2DBC drivers fully implement the database wire protocol on top of a non-blocking I/O layer.

# Design Principles

R2DBC aims for a minimal SPI surface, specifying only parts that differ across databases, and is fully reactive and backpressure-aware all the way down to the database. It is intended primarily as a driver SPI to be consumed by client libraries and not intended to be used directly in application code.

# Cloud Ready

R2DBC supports [cloud native](https://pivotal.io/cloud-native) applications using relational databases such as PostgreSQL, MySQL, and others. Application developers are free to pick the right database for the job without being confined by APIs.

# Community

While led by members of the Spring team at Pivotal, R2DBC depends upon community support. We invite contributors from all relational data stores to participate in building a reactive relational future.
