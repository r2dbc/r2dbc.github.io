---
layout: default
---

R2DBC is an endeavor to bring a reactive programming API to relational data stores. It was first announced at SpringOne Platform 2018, as shown in the keynote below:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/E3s5f-JF8z4?start=520" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

From the same conference, see Ben Hale go into details of what reactive relational access means. Also discover what it's like to build [clients](/clients) and [drivers](/drivers):

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/idApf9DMdfk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# [Three-columns]

## [Column 1]Reactive Streams

R2DBC is founded on **Reactive Streams** providing an **asynchronous**, **non-blocking** API.

## [Column 2]Relational Databases

R2DBC engages **relational** databases with a **reactive API**, something not possible with the blocking nature of JDBC and JPA.

## [Column 3]Scalable Solutions

Reactive Streams makes it possible to move from the classic one thread per connection approach to a more **powerful**, more **scalable** approach.

# Relational meets reactive [align:left]

[TODO: graphic] People wanting to scale while retaining usage of relational databases are cut off from reactive programming due to existing standards. R2DBC introduces a new API that allows asynchronous, non-blocking code that work efficiently with relational databases.

# Project Reactor [align:right]

[TODO: graphic] [Project Reactor](http://projectreactor.io), Pivotal's implementation of Reactive Streams, merges reactive backpressure with functional programming. Reactor makes it easy to connect the most tried and true database engines with a scalable API.

# Community [align:left]

[TODO: graphic] While led by members of the Spring team at Pivotal, R2DBC depends upon community support. Contributors from all relational data stores are invited to participate in building a reactive, relational future.