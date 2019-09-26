---
layout: default
---

R2DBC (Reactive Relational Database Connectivity) is an endeavor to bring a reactive programming API to SQL databases. It was first announced at SpringOne Platform 2018, as shown in the keynote below:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/E3s5f-JF8z4?start=520" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# In a Nutshell

* **Reactive Streams** - R2DBC is founded on **Reactive Streams** providing a fully **reactive** **non-blocking** API.
* **Relational Databases** - R2DBC engages **SQL** databases with a **reactive API**, something not possible with the blocking nature of JDBC.
* **Scalable Solutions** - Reactive Streams makes it possible to move from the classic one thread per connection approach to a more **powerful**, more **scalable** approach.
* **Open Specification** - R2DBC is an open specification establishing a SPI that driver vendors can implement and clients can consume.

# Features

* Broad type conversion
* Transactions, Isolation Levels, Save points
* Batching
* BLOB/CLOB
* Connection URLs
* Java ServiceLoader-based `ConnectionFactory` discover and configuration
* Observability

## [Driver Implementations](/drivers/)

* [cloud-spanner-r2dbc](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc) - Driver for Google Cloud Spanner
* [jasync-sql](https://github.com/jasync-sql/jasync-sql) - R2DBC wrapper for Java & Kotlin Async Database Driver for MySQL and PostgreSQL written in Kotlin.
* [r2dbc-h2](https://github.com/r2dbc/r2dbc-h2) - Native driver implemented for H2 as a test database.
* [r2dbc-postgres](https://github.com/r2dbc/r2dbc-postgresql) - Native driver implemented for PostgreSQL.
* [r2dbc-mssql](https://github.com/r2dbc/r2dbc-mssql) - Native driver implemented for Microsoft SQL Server.
* [r2dbc-mysql](https://github.com/mirromutth/r2dbc-mysql) - Native driver implemented for MySQL.

## Connection Pooling

Provided through the reactive connection pool implementation in [`r2dbc-pool`](https://github.com/r2dbc/r2dbc-pool).

## Observability

Provided through [`r2dbc-proxy`](https://github.com/r2dbc/r2dbc-proxy).

# Relational meets Reactive

People wanting to scale while retaining usage of relational databases are cut off from reactive programming due to existing standards based on blocking I/O. R2DBC specifies a new API that allows reactive code that work efficiently with relational databases.

R2DBC is a specification designed from the ground up for reactive programming with SQL databases defining a non-blocking SPI for database driver implementors and client library authors. R2DBC drivers implement fully the database wire protocol on top of a non-blocking I/O layer.

# Design Principles

R2DBC aims for a minimal SPI surface specifying only parts that differ across databases. It is fully reactive and backpressure-aware all the way down to the database. It is intended primarily as driver SPI to be consumed by client libraries and not intended to be used directly from application code.

# Cloud Ready

R2DBC supports [cloud native](https://pivotal.io/cloud-native) apps where relational databases like PostgreSQL, MySQL, and others are found. Have the freedom to pick the right one for the job and not be confined by API.

# Community

While led by members of the Spring team at Pivotal, R2DBC depends upon **community support**. Contributors from all relational data stores are invited to participate in building a reactive, relational future.

