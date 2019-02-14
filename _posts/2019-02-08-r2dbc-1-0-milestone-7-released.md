---
layout: post
title:  "R2DBC 1.0 Milestone 7 released"
date:   2019-02-08 18:09:00 -0600
tags: [milestone, release]
author: Mark Paluch
---

Greetings R2DBC community!

We are delighted to announce the availability of R2DBC 1.0.0.M7, the seventh milestone release. 
The release is available from [https://repo.spring.io/milestone/](https://repo.spring.io/milestone/) and ships with a few new modules:
**R2DBC Proxy** and a Bill of Materials.

Introducing the Bill of Materials (bom) simplifies version management and consumption.
Each project has its own theme how it names release trains. Want to hear a bit of trivia?
We love Italy. We love the [Dolomites](https://en.wikipedia.org/wiki/Dolomites) and so name our release trains after Dolomiti towns. The first release train is named: [Arabba](https://en.wikipedia.org/wiki/Arabba). So let us introduce you to `Arabba-M7`.

We are also excited to announce that this is the first release shipping with [R2DBC Proxy](https://github.com/r2dbc/r2dbc-proxy)  covering a multitude of use cases that are solved best with decoration: Tracing, Metrics, Observability. 

The release train ships with the following modules:
* R2DBC SPI (`io.r2dbc:r2dbc-spi`, `io.r2dbc:r2dbc-spi-test`)
* R2DBC Client (`io.r2dbc:r2dbc-client`)
* R2DBC PostgreSQL driver (`io.r2dbc:r2dbc-postgresql`)
* R2DBC H2 driver (`io.r2dbc:r2dbc-h2`)
* R2DBC Microsoft SQL Server driver (`io.r2dbc:r2dbc-mssql`)

New modules in this release:
* R2DBC Proxy (`io.r2dbc.r2dbc-proxy`)
* R2DBC BOM (`io.r2dbc.r2dbc-bom`)

Most notable SPI changes are: 

* Reinstated generated value (key) retrieval (`Statement.returnGeneratedValues(…)`) that moves key generation back to the driver.
* Improved support for column metadata (`ColumnMetadata`).
* Add support for `ConnectionFactory` discovery allowing connection creation without using driver-specific API.
* R2DBC ships with specification documentation. 

**[Release artifacts](/spec/1.0.0.M7/)**

* [Binaries](https://repo.spring.io/milestone/io/r2dbc/)
* [Javadoc](/spec/1.0.0.M7/api/)
* [Specification](/spec/1.0.0.M7/spec/html/)
* [Changelog](/spec/1.0.0.M7/CHANGELOG.txt)

To access to this release, include our milestone repository to access R2DBC 1.0 M7. If you use Maven, then add the following lines to your `pom.xml`:

```xml

<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-M7</version>
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

<repository>
  <id>spring-milestones</id>
  <name>Spring Milestones</name>
  <url>https://repo.spring.io/milestone</url>
</repository>
```


Don't forget to join the [community](/resources).

Cheers!