---
layout: default
---

R2DBC is an endeavor to bring a reactive programming API to relational data stores. It was first announced at SpringOne Platform 2018, as shown in the keynote below:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/E3s5f-JF8z4?start=520" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

From the same conference, see Ben Hale go into details of what reactive relational access means. Also discover what it's like to build [clients](/clients) and [drivers](/drivers):

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/idApf9DMdfk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# Reactive Streams

R2DBC is rooted in [Reactive Streams](http://www.reactive-streams.org/). Reactive Streams defines **asynchronous**, **non-blocking** interactions between components. Instead of using a thread per connection, industry experience reveals that smaller pools of threads, even a single thread, used in a non-blocking fashion, yields higher throughput.

People wanting to scale while retaining usage of relational databases are cut off from this programming model due to JDBC and JPA being blocking APIs. Blocking APIs do not work in a reactive environment.

# Project Reactor

[Project Reactor](http://projectreactor.io) is Pivotal's implementation of Reactive Streams. It takes Reactive Stream's concept of **backpressure** and merges it with **functional programming**. 

The ability to declare "what" to do using Java 8 lambdas and method handles, while letting Reactor decide "when" and "how" to execute gives programmers the ability to build scalable systems.

# Community

While led by members of the Spring team at Pivotal, R2DBC depends upon community support. That's why contributors from all relational data stores are invited to participate in building a reactive, relational future.