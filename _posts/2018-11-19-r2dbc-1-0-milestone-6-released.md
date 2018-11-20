---
layout: post
title:  "R2DBC 1.0 Milestone 6 released"
date:   2018-11-19 11:09:00 -0600
tags: [milestone, release]
author: Mark Paluch
---

Greetings R2DBC community!

We're pleased to announce the availability of R2DBC 1.0 M6. The release is available from [https://repo.spring.io/milestone/](https://repo.spring.io/milestone/) and ships with two new database drivers: **H2** and **Microsoft SQL Server**.

This release is, in fact, a release train that comes with multiple modules:

* R2DBC SPI (`io.r2dbc.r2dbc-spi`, `io.r2dbc.r2dbc-spi-test`)
* R2DBC Client (`io.r2dbc.r2dbc-client`)
* R2DBC PostgreSQL driver (`io.r2dbc.r2dbc-postgresql`)

New modules in this release:

* R2DBC H2 driver (`io.r2dbc.r2dbc-h2`)
* R2DBC Microsoft SQL Server driver (`io.r2dbc.r2dbc-mssql`)

Most notable SPI changes are: 

* Removal of `Statement.executeReturningGeneratedKeys()`: Retrieval of generated keys is moved out of the SPI and consequently the drivers. This is a responsibility better suited for client implementations.
* Removal of `Connection.setTransactionMutability(…)`: In JDBC, transaction mutability (read-only/read-write) is inconsistently supported. Even the spec states that it's a hint and not a required behavior. So we removed it from the SPI.
* Addition of `Statement.bind(int, …)` and `Statement.bindNull(int, Class<?>)` methods to bind statement parameters by index.

It's important to note that you can set most parameters (such as transaction mutability hints, transaction isolation levels) by issuing the proper SQL statements to your database server.

To access to this release, include our milestone repository to access R2DBC 1.0 M6. If you use Maven, then add the following lines to your `pom.xml`:

```xml
<repository>
    <id>spring-milestones</id>
    <name>Spring Milestones</name>
    <url>https://repo.spring.io/milestone</url>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

Don't forget to join the [community](/resources).

Cheers!