---
layout: page
title: Clients
permalink: /clients/
---

R2DBC encourages libraries to provide a "humane" API in form of a client library. R2DBC avoids implementing user-space features in each driver and rather leaves this up to specific client implementations.

If you're eager to start using R2DBC to build an application, check out the [existing clients](#existing-clients) listed below. If you're interested in crafting your own client, check out the section on [new clients](#new-clients) further down.

## Existing clients

* [r2dbc-client](https://github.com/r2dbc/r2dbc-client) - client using pure Reactor (i.e. no Spring dependencies).
* [spring-data-r2dbc](https://github.com/spring-projects/spring-data-r2dbc) - Spring Data client for R2DBC.

## Client Development under Investigation

* [MyBatis (#1444)](https://github.com/mybatis/mybatis-3/issues/1444)
* [JDBI (#1454)](https://github.com/jdbi/jdbi/issues/1454)
* [jOOQ (#6298)](https://github.com/jOOQ/jOOQ/issues/6298)
* [Querydsl (#2468)](https://github.com/querydsl/querydsl/issues/2468)
* [Helidon (#581)](https://github.com/oracle/helidon/issues/581)
* [Liquibase (CORE-3419)](https://liquibase.jira.com/browse/CORE-3419)
* [Flyway (#2502)](https://github.com/flyway/flyway/issues/2502)
* [Exposed (#456)](https://github.com/JetBrains/Exposed/issues/456)
* [Testcontainers (#1003)](https://github.com/testcontainers/testcontainers-java/issues/1003)

## Writing a Client

R2DBC's minimal SPI makes it easy to write a client. The modules above can provide inspiration if you wish to write a different client for the community.

To write a custom client, R2DBC's [`ConnectionFactory`](https://github.com/r2dbc/r2dbc-spi/blob/master/r2dbc-spi/src/main/java/io/r2dbc/spi/ConnectionFactory.java) , [`Connection`](https://github.com/r2dbc/r2dbc-spi/blob/master/r2dbc-spi/src/main/java/io/r2dbc/spi/Connection.java) , and [`Statement`](https://github.com/r2dbc/r2dbc-spi/blob/master/r2dbc-spi/src/main/java/io/r2dbc/spi/Statement.java) SPI provides you the necessary building blocks.

The SPI can be found at:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi**

This artifact contains R2DBC's `Connection` interface (and others) which you can wrap up inside your client.
