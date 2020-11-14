---
layout: page
title: Clients
permalink: /clients/
---

R2DBC encourages libraries to provide a "humane" API in the form of a client library. R2DBC avoids implementing user-space features in each driver, and leaves these for specific clients to implement.

If you're eager to start using R2DBC to build an application, check out the [existing clients](#existing-clients) listed below. If you're interested in crafting your own client, check out the section on [new clients](#new-clients) further down.

## Existing Clients

* [r2dbc-client](https://github.com/r2dbc/r2dbc-client) - client using pure Reactor (i.e. no Spring dependencies).
* [spring-data-r2dbc](https://github.com/spring-projects/spring-data-r2dbc) - Spring Data client for R2DBC.
* [Kotysa](https://github.com/pull-vert/kotysa) - Typesafe and Co-routine-ready SQL engine using Kotlin.
* [jOOQ](https://www.jooq.org/doc/3.13/manual/sql-execution/fetching/reactive-fetching/) - a fluent API for typesafe SQL query construction library.
* [Testcontainers](https://www.testcontainers.org/modules/databases/r2dbc/) - support to connect and bootstrap a database in a Testcontainer.

## Client Development Under Investigation

* MyBatis ([#1444](https://github.com/mybatis/mybatis-3/issues/1444))
* JDBI ([#1454](https://github.com/jdbi/jdbi/issues/1454))
* jOOQ ([#6298](https://github.com/jOOQ/jOOQ/issues/6298))
* Querydsl ([#2468](https://github.com/querydsl/querydsl/issues/2468))
* Helidon ([#581](https://github.com/oracle/helidon/issues/581))
* Liquibase ([CORE-3419](https://liquibase.jira.com/browse/CORE-3419))
* Flyway ([#2502](https://github.com/flyway/flyway/issues/2502))
* Exposed ([#456](https://github.com/JetBrains/Exposed/issues/456))

## Writing a Client

R2DBC's minimal SPI makes it easy to write a client, and the clients listed above can provide inspiration if you wish to write a different client for the community. You can find the SPI at:

* **Group** `io.r2dbc`
* **Artifact** `r2dbc-spi`

This artifact contains R2DBC's `Connection` interface (and others), which you can wrap from within your client. The R2DBC [`ConnectionFactory`](https://github.com/r2dbc/r2dbc-spi/blob/main/r2dbc-spi/src/main/java/io/r2dbc/spi/ConnectionFactory.java), [`Connection`](https://github.com/r2dbc/r2dbc-spi/blob/main/r2dbc-spi/src/main/java/io/r2dbc/spi/Connection.java), and [`Statement`](https://github.com/r2dbc/r2dbc-spi/blob/main/r2dbc-spi/src/main/java/io/r2dbc/spi/Statement.java) SPIs provide you the necessary building blocks for writing a custom client.
