---
layout: post
title:  "R2DBC Arabba-SR12 released"
date:   2022-01-13 08:00:00 +0200
tags: [release]
author: Mark Paluch
---

On behalf of the community and everyone who contributed, we're pleased to announce availability of R2DBC `Arabba-SR12` available from Maven Central!

This service release ships the following modules:

* [Google Cloud Spanner Driver - 1.1.0](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc/releases/tag/v1.1.0) (`com.google.cloud:cloud-spanner-r2dbc`)
* MariaDB connector - 1.0.3 (`org.mariadb:r2dbc-mariadb`)
* [H2 driver - 0.8.5.RELEASE](https://github.com/r2dbc/r2dbc-h2/milestone/11?closed=1)  (`io.r2dbc:r2dbc-h2`)
* [PostgreSQL driver - 0.8.11.RELEASE](https://github.com/pgjdbc/r2dbc-postgresql/milestone/22?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [R2DBC Pool - 0.8.8.RELEASE](https://github.com/r2dbc/r2dbc-pool/milestone/14?closed=1)  (`io.r2dbc:r2dbc-pool`)
* [SQL Server driver - 0.8.8.RELEASE](https://github.com/r2dbc/r2dbc-mssql/milestone/16?closed=1)  (`io.r2dbc:r2dbc-postgresql`)

This is a maintenance release shipping with mostly bugfixes fixes, selected enhancements, and dependency upgrades. Check out the changelogs associated with each component.

We recommend version management by using R2DBC BOM as individual modules follow their own version number schedule.

If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-SR12</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>cloud-spanner-r2dbc</artifactId>
  </dependency>
</dependencies>
```
