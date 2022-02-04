---
layout: post
title:  "R2CBC Borca-RELEASE released"
date:   2022-02-04 08:00:00 +0200
tags: [release]
author: Mark Paluch
---

It is my pleasure to announce that, after more than two years of specification work, milestones and RCs we can finally conclude the efforts of R2DBC 0.9 with the Borca release train being generally available from Maven Central.

The release train bundles the R2DBC 0.9 specification and all compliant implementations within a release train by providing a bill of materials to ensure a consistent set of dependencies for your reactive SQL database workloads.

Specifically, this release train ships with:

* `io.r2dbc:r2dbc-spi:0.9.1.RELEASE` - [R2DBC SPI 0.9.1.RELEASE](https://r2dbc.io/2021/12/06/r2dbc-0.9.0-goes-ga)
* `io.r2dbc:r2dbc-h2:0.9.1.RELEASE` - [R2DBC H2 driver 0.9.1.RELEASE](https://github.com/r2dbc/r2dbc-h2/releases/tag/v0.9.1.RELEASE)
* `org.mariadb:r2dbc-mariadb:1.1.1-rc` - [MariaDB R2DBC connector 1.1.1-rc](https://github.com/mariadb-corporation/mariadb-connector-r2dbc)
* `com.oracle.database.r2dbc:oracle-r2dbc:0.4.0` - [Oracle R2DBC driver 0.4.0](https://github.com/oracle/oracle-r2dbc/releases/tag/0.4.0)
* `io.r2dbc:r2dbc-pool:0.9.0.RELEASE` - [R2DBC Pool 0.9.0.RELEASE](https://github.com/r2dbc/r2dbc-pool/releases/tag/v0.9.0.RELEASE)
* `org.postgresql:r2dbc-postgres:0.9.0.RELEASE` - [R2DBC Postgres driver 0.9.0.RELEASE](https://github.com/pgjdbc/r2dbc-postgresql/releases/tag/v0.9.0.RELEASE)
* `io.r2dbc:r2dbc-proxy:0.9.0.RELEASE` - [R2DBC Proxy 0.9.0.RELEASE](https://github.com/r2dbc/r2dbc-proxy/releases/tag/v0.9.0.RELEASE)
* `io.r2dbc:r2dbc-mssql:0.9.0.RELEASE` - [R2DBC SQL Server driver 0.9.0.RELEASE](https://github.com/r2dbc/r2dbc-mssql/releases/tag/v0.9.0.RELEASE)

If you use Maven, you can add the following lines to your pom.xml:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Borca-RELEASE</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>r2dbc-postgres</artifactId>
  </dependency>
</dependencies>
```

With the transition of the Borca release train to GA, we plan to ship two final rounds of service releases for the `Arabba` release train (R2DBC 0.8) later this year before transitioning the `Arabba` release train into EOL mode after Q2/2022. Each implementation can decide whether they are going to ship maintenance releases supporting R2DBC 0.8.
We are also working towards R2DBC 1.0 GA. The backlog is sorted and the 1.0 GA release is going to be a lighter revision of the specification where we iron out any last rough edges. R2DBC 1.0 is going to be the version that serves as reactive database integration spec for the foreseeable future.