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

This service release includes updates to:

* [R2DBC PostgreSQL driver - 0.8.5.RELEASE](https://github.com/pgjdbc/r2dbc-postgresql/milestone/14?closed=1)  (`io.r2dbc:r2dbc-postgresql`)
* [R2DBC Pool - 0.8.4.RELEASE](https://github.com/r2dbc/r2dbc-pool/milestone/9?closed=1) (`io.r2dbc:r2dbc-pool`)

This is a maintenance release with patches and fixes, but nothing breaking. Feel free to check the ticket logs above for the module you're interested in.

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
