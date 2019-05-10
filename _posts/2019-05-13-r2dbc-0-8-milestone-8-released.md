---
layout: post
title:  "R2DBC 0.8 Milestone 8 released"
date:   2019-05-13 20:00:00 +0100
tags: [milestone, release]
author: Mark Paluch
---

On behalf of the R2DBC community, I'm pleased to announce the availability of R2DBC 0.8.0 M8 (Arabba-M8).

If you have followed R2DBC development, your first question may be: Wasn't the last release 1.0.0.M7? Yes, it was. So why is this one 0.8.0?

We decided to switch to 0.x versions for two reasons:

1. We're paving pathway to production aiming for a GA release.
2. At the same time, we want to express that the SPI can be subject to changes and that it is not yet immutable.

We already have a few tickets lined up for the next milestone, and we know that they will require further SPI modifications:

1. Support for Auto-Commit
2. Connection Validation
3. Support for Stored Procedures

Once we feel that our SPI is stable, such that we can guarantee backward-compatible changes only, we will ship a 1.0 release.

We are also excited to announce R2DBC Pool, adding reactive connection pooling to your application. Another great news item to share is that the community has picked up on R2DBC by providing an R2DBC wrapper for [jasync-sql's MySQL driver](https://github.com/jasync-sql/jasync-sql), so you can now use MySQL through R2DBC.

This SPI release is packed with new enhancements:

* Connection URL Parsing through `ConnectionFactories.get(String)`
* Support for Large Object streaming through `Blob` and `Clob` types
* Categorized Exception Hierarchy
* Extended `RowMetadata`
* Extensible `IsolationLevel` constants for vendor-specific isolation levels
* Extended specification document
* Extensions to R2DBC TCK

On the driver side, we have:

* Implementations of BLOB and CLOB support and categorized exceptions
* Binary transfer for R2DBC PostgreSQL
* Support of PLP-encoded types and configurable direct and cursored execution modes for SQL Server
* UUID Codec, index-based binding, and `java.time` support for H2

The release train ships with the following modules:

* R2DBC SPI (`io.r2dbc:r2dbc-spi`, `io.r2dbc:r2dbc-spi-test`)
* R2DBC Client (`io.r2dbc:r2dbc-client`)
* R2DBC PostgreSQL driver (`io.r2dbc:r2dbc-postgresql`)
* R2DBC H2 driver (`io.r2dbc:r2dbc-h2`)
* R2DBC Microsoft SQL Server driver (`io.r2dbc:r2dbc-mssql`)
* R2DBC Proxy (`io.r2dbc:r2dbc-proxy`)
* R2DBC BOM (`io.r2dbc:r2dbc-bom`)

New modules in this release:

* R2DBC Pool (`io.r2dbc:r2dbc-pool`)

Release artifacts

* [Binaries](https://repo.spring.io/milestone/io/r2dbc/)
* [Javadoc](http://r2dbc.io/spec/0.8.0.M8/api/)
* [Specification](http://r2dbc.io/spec/0.8.0.M8/spec/html/)
* [Changelog](http://r2dbc.io/spec/0.8.0.M8/CHANGELOG.txt)

To access this release, make sure to include our milestone repository to get access R2DBC 0.8 M8. If you use Maven, you can add the following lines to your pom.xml:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-M8</version>
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
</dependencies>

<dependencies>
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
