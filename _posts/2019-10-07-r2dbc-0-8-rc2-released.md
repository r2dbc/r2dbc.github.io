---
layout: post
title:  "R2DBC 0.8 Release Candidate 2 released"
date:   2019-10-07 11:00:00 -0500
tags: [milestone, release]
author: Mark Paluch
---

On behalf of the R2DBC community, I'm pleased to announce the availability of R2DBC 0.8.0 RC2 (Arabba-RC2).

This release addresses specific dependency issues with Reactor Netty avoiding netty dependency exclusions with Postgres and SQL Server drivers.

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
* [Javadoc](http://r2dbc.io/spec/0.8.0.RC2/api/)
* [Specification](http://r2dbc.io/spec/0.8.0.RC2/spec/html/)
* [Changelog](http://r2dbc.io/spec/0.8.0.RC2/CHANGELOG.txt)

To access this release, make sure to include our milestone repository to get access R2DBC 0.8 RC2. If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-RC2</version>
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
