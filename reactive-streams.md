---
layout: page
title: Concepts
permalink: /concepts/
---

R2DBC is built on several key concepts.


# Reactive Streams

R2DBC is first and foremost built on Reactive Streams.

[Reactive Streams](http://www.reactive-streams.org/) is a spec that defines asynchronous, non-blocking interactions between components, whether co-located or spread across multiple services.

What does this mean?

* **asynchronous** - The answer isn't coming immediately. It could be milliseconds. It could be hours.
* **non-blocking** - While you wait for that asynchronous answer, don't hold up a thread. Instead, let that thread process other requests work.

We've learned that having 100, 200, 500 threads is actually not very effective. In fact, more threads than the number of cores on your machine doesn't scale. Instead, it's better to have a small thread pool, sometimes even just one thread, and to instead use tactics like [work stealing](https://en.wikipedia.org/wiki/Work_stealing) to support non-blocking solutions.

As mentioned in [Ollie's keynote](/), the Java standards for accessing relational databases, JDBC and JPA, are synchronous and blocking. Many shops that would like to embrace reactive programming simply can't due to this limitation.

# Project Reactor

[Project Reactor](http://projectreactor.io) is Pivotal's implementation of Reactive Streams (a spec not aimed at everyday developers). Reactive Streams itself is a very low level API that defines **backpressure**, the ability to push back and only accept as much work as your ready for.

Project Reactor builds on top of Java 8, leveraging functional programming (FP) concepts. Combined with reactive programming, it packs a punch. The ability to declare a "recipe" of what to do, while letting the framework decide "when" and "how" to execute it, programmers are suddenly able to build more scalable systems.

# Traditional Databases

Most of the drivers available to Java developers are built under the assumption of JDBC or JPA access. This is perfectly understandable given the climate of the Java ecosystem.
