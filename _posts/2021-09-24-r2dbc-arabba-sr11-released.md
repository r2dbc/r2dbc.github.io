---
layout: post
title:  "R2DBC Arabba-SR11 released"
date:   2021-09-24 08:00:00 +0200
tags: [release]
author: Mark Paluch
---

On behalf of the community and everyone who contributed, we're pleased to announce availability of R2DBC `Arabba-SR11` available from Maven Central!

This service release ships the following modules:

* [R2DBC Specification - 0.8.6.RELEASE](https://github.com/r2dbc/r2dbc-spi/milestone/15?closed=1)  (`io.r2dbc:r2dbc-spi`)
* [Google Cloud Spanner Driver - 0.6.0](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc/releases/tag/v0.6.0) (`com.google.cloud:cloud-spanner-r2dbc`)
* [MariaDB connector - 1.0.2](https://github.com/mariadb-corporation/mariadb-connector-r2dbc/releases/tag/1.0.2) (`org.mariadb:r2dbc-mariadb`)
* [PostgreSQL driver - 0.8.10.RELEASE](https://github.com/pgjdbc/r2dbc-postgresql/milestone/19?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [SQL Server driver - 0.8.7.RELEASE](https://github.com/r2dbc/r2dbc-mssql/milestone/14?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [R2DBC Proxy - 0.8.8.RELEASE](https://github.com/r2dbc/r2dbc-proxy/milestone/14?closed=1)  (`io.r2dbc:r2dbc-proxy`)


This is a maintenance release shipping with mostly bugfixes fixes, selected enhancements, and dependency upgrades. Check out the changelogs associated with each component.

We recommend version management by using R2DBC BOM as individual modules follow their own version number schedule.

If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-SR11</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.mariadb</groupId>
    <artifactId>r2dbc-mariadb</artifactId>
  </dependency>
</dependencies>
```
