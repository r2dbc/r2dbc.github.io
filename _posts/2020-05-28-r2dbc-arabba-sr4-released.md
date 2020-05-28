---
layout: post
title:  "R2DBC Arabba-SR4 released"
date:   2020-05-28 11:05:00 -0600
tags: [release]
author: Greg Turnquist
---

Dear community,

It is my pleasure to announce that R2DBC has released it's fourth service release, `Arabba-SR4` from Maven Central!

R2DBC enables the Java platform with a reactive, non-blocking way to access relational databases via SQL.

This service release includes updates to:

* [R2DBC SPI - 0.8.2.RELEASE](https://github.com/r2dbc/r2dbc-spi/milestone/10?closed=1) (`io.r2dbc:r2dbc-spi`)
* [R2DBC H2 - 0.8.4.RELEASE](https://github.com/r2dbc/r2dbc-h2/milestone/10?closed=1) (`io.r2dbc:r2dbc-h2`)
* [R2DBC Microsoft SQL Server driver - 0.8.3.RELEASE](https://github.com/r2dbc/r2dbc-mssql/milestone/9?closed=1) (`io.r2dbc:r2dbc-mssql`)
* [R2DBC PosgreSQL driver - 0.8.3.RELEASE](https://github.com/r2dbc/r2dbc-postgresql/milestone/12?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [R2DBC Pool - 0.8.3.RELEASE](https://github.com/r2dbc/r2dbc-pool/milestone/8?closed=1) (`io.r2dbc:r2dbc-pool`)

This is a maintenance release with patches and fixes, but nothing breaking. Feel free to check the ticket logs above for the module you're interested in.

A few resources with details about this release:

* [Introduction into R2DBC](https://www.youtube.com/watch?v=kKyiLcFFe2E)
* [Javadoc](https://r2dbc.io/spec/0.8.2.RELEASE/api/)
* [R2DBC Specification](https://r2dbc.io/spec/0.8.2.RELEASE/spec/html/)

We recommend version management by using R2DBC BOM as individual modules follow their own version number schedule.

### Release artifacts

* [Binaries](http://repo1.maven.org/maven2/io/r2dbc/)
* [Javadoc](http://r2dbc.io/spec/0.8.2.RELEASE/api/)
* [Specification](http://r2dbc.io/spec/0.8.2.RELEASE/spec/html/)
* [Changelog](http://r2dbc.io/spec/0.8.2.RELEASE/CHANGELOG.txt)

If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-SR4</version>
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
```

### Next Steps

R2DBC 0.8 is the first release of the open standard. We're expecting maintenance releases shipping minor revisions of the specification and drivers over the course of the next months. 
We're looking towards a 0.9 revision of R2DBC: Stored procedures, extensions to transaction definitions, and a specification for database events are only a few topics planned for the next iteration.
Join the [community](https://r2dbc.io/resources) to get involved and to follow development closely.

Cheers, 

Greg