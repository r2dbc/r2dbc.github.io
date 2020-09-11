---
layout: post
title:  "R2DBC Arabba-SR7 released"
date:   2020-09-10 11:26:00 -0600
tags: [release]
author: Greg Turnquist
---

Dear community,

It is my pleasure to announce that R2DBC has released it's seventh service release, `Arabba-SR7` from Maven Central!

R2DBC enables the Java platform with a reactive, non-blocking way to access relational databases via SQL.

We are excited to announce that this version includes the R2DBC MariaDB connector:

* [R2DBC MariaDB connector - 0.8.3.RELEASE](https://github.com/mariadb-corporation/mariadb-connector-r2dbc/releases/tag/0.8.3) (`org.mariadb:r2dbc-mariadb`)

This service release ships also updates to:

* [R2DBC PostgreSQL driver - 0.8.5.RELEASE](https://github.com/pgjdbc/r2dbc-postgresql/milestone/14?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [R2DBC Pool - 0.8.4.RELEASE](https://github.com/r2dbc/r2dbc-pool/milestone/9?closed=1) (`io.r2dbc:r2dbc-pool`)

This is a maintenance release shipping with mostly bugfixes fixes, selected enhancements, and dependency upgrades. Check out the changelogs associated with each component.

Check out this latest video, where Greg Turnquist presents R2DBC to the Atlanta JUG:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/t7oLx9RJkB8?start=352" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

We recommend version management by using R2DBC BOM as individual modules follow their own version number schedule.

If you use Maven, you can add the following lines to your `pom.xml`:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.r2dbc</groupId>
      <artifactId>r2dbc-bom</artifactId>
      <version>Arabba-SR7</version>
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

Cheers, 

Greg
