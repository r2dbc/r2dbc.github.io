---
layout: post
title:  "R2DBC 0.8 Release Candidate 1 released"
date:   2019-09-26 18:00:00 +0100
tags: [milestone, release]
author: Mark Paluch
---

On behalf of the R2DBC community, I'm pleased to announce the availability of R2DBC 0.8.0 RC1 (Arabba-RC1).

The first release candidate comes with several additions to the SPI and enhancements to driver implementations.
This almost six-month-long iteration introduced the final, required additions to R2DBC to satisfy requirements from various integration perspectives.
Several changes needed to be reflected in the specification to cater for:  

* Transaction Management
* Connection Pooling
* Application Health Observability
* Database Migration Tooling

The R2DBC specification is now feature-complete for 0.8.0.

The most notable changes in R2DBC SPI are (amongst many others):

* Positional and named parameter binding/value retrieval in `Statement` respective `Row`.
* Vendor-independent connection validation.
* Connection metadata exposing details about the connected database. 
* Specification for Auto-Commit and `IsolationLevel` behavior.

On the driver side, we have:

* Benchmarks for H2, PostgreSQL, and SQL Server drivers.
* Removal of performance regressions and memory leaks.
* Implementation of all specification-mandated changes.
* R2DBC H2 supports H2's Geometry data types when Locationtech's JTS is on the classpath, remote H2 instances via TCP, and a streamlined API to create an in-memory database without the need to specify exit and DB close behavior (`DB_CLOSE_DELAY`, `DB_CLOSE_ON_EXIT`).
* R2DBC PostgreSQL supports `LISTEN`/`NOTIFY` notifications, SSL-encrypted connections, extension points for 3rd-party `Codec` implementations for e.g. AgensGraph or PostGIS usage, and supports Postgres' JSON and JSONB types.
* R2DBC SQL Server can now be fully operated on Microsoft Azure considering hostname specifics in SSL certificates and supports byte arrays for `VARBINARY` greater 65kb.

We're working with R2DBC towards a 0.8.0 GA release later this year. 
Based on the feedback we are able to collect from RC1 we will decide whether we require another release candidate or whether we can ship directly 0.8.0.RELEASE.

The release train ships with the following modules:

* R2DBC BOM (`io.r2dbc:r2dbc-bom`)
* R2DBC Client (`io.r2dbc:r2dbc-client`)
* R2DBC H2 driver (`io.r2dbc:r2dbc-h2`)
* R2DBC Microsoft SQL Server driver (`io.r2dbc:r2dbc-mssql`)
* R2DBC Pool (`io.r2dbc:r2dbc-pool`)
* R2DBC PostgreSQL driver (`io.r2dbc:r2dbc-postgresql`)
* R2DBC Proxy (`io.r2dbc:r2dbc-proxy`)
* R2DBC SPI (`io.r2dbc:r2dbc-spi`, `io.r2dbc:r2dbc-spi-test`)

Release artifacts

* [Binaries](https://repo.spring.io/milestone/io/r2dbc/)
* [Javadoc](http://r2dbc.io/spec/0.8.0.RC1/api/)
* [Specification](http://r2dbc.io/spec/0.8.0.RC1/spec/html/)
* [Changelog](http://r2dbc.io/spec/0.8.0.RC1/CHANGELOG.txt)

To access this release, make sure to include our milestone repository to get access R2DBC 0.8 RC1. If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-RC1</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>io.r2dbc</groupId>
    <artifactId>r2dbc-postgresql</artifactId>
  </dependency>

  <dependency>
    <groupId>io.r2dbc</groupId>
    <artifactId>r2dbc-pool</artifactId>
  </dependency>
</dependencies>

<repository>
  <id>spring-milestones</id>
  <name>Spring Milestones</name>
  <url>https://repo.spring.io/milestone</url>
</repository>
```

Don’t forget to join the [community](http://r2dbc.io/resources).

Cheers!
