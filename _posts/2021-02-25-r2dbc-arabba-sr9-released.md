---
layout: post
title:  "R2DBC Arabba-SR9 released"
date:   2021-02-25 16:00:00 +0200
tags: [release]
author: Mark Paluch
---

On behalf of the community and everyone who contributed, we're pleased to announce availability of R2DBC `Arabba-SR9` available from Maven Central!

This service release ships the following modules:

* [Google Cloud Spanner Driver - 0.3.0](https://github.com/GoogleCloudPlatform/cloud-spanner-r2dbc/milestone/2?closed=1) (`com.google.cloud:cloud-spanner-r2dbc`)
* [MariaDB connector - 1.0.0](https://github.com/mariadb-corporation/mariadb-connector-r2dbc/commit/4e6a18ac0975f34d8de1808854d47e574c5e2d32) (`org.mariadb:r2dbc-mariadb`)
* [PostgreSQL driver - 0.8.6.RELEASE](https://github.com/pgjdbc/r2dbc-postgresql/milestone/16?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [R2DBC Pool - 0.8.6.RELEASE](https://github.com/r2dbc/r2dbc-pool/milestone/10?closed=1) (`io.r2dbc:r2dbc-pool`)
* [R2DBC Proxy - 0.8.5.RELEASE](https://github.com/r2dbc/r2dbc-proxy/milestone/10?closed=1)  (`io.r2dbc:r2dbc-proxy`)


This is a maintenance release shipping with mostly bugfixes fixes, selected enhancements, and dependency upgrades. Check out the changelogs associated with each component.

We recommend version management by using R2DBC BOM as individual modules follow their own version number schedule.

If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-SR9</version>
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
