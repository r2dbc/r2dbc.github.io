---
layout: default
---

R2DBC is an endeavor to bring a reactive programming API to relational data stores. It was first announced at SpringOne Platform 2018, as shown in the keynote below:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/E3s5f-JF8z4?start=520" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>


From the same conference, see Ben Hale go into details of what reactive relational access means. Also discover what it's like to build [clients](/clients) and [drivers](/drivers):

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/idApf9DMdfk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

* **Reactive Streams** - R2DBC is founded on **Reactive Streams** providing an **asynchronous**, **non-blocking** API.
* **Relational Databases** - R2DBC engages **relational** databases with a **reactive API**, something not possible with the blocking nature of JDBC and JPA.
* **Scalable Solutions** - Reactive Streams makes it possible to move from the classic one thread per connection approach to a more **powerful**, more **scalable** approach.

# Features

| Feature Matrix                | H2 (in-memory) | PostgreSQL | MS SQL Server |
| ----------------------------- | -------------- | ---------- | ------------- |
| Connection pooling            |                |            |               |
| Broad type conversion         | X              |     X      |      X        |
| Transactions                  | X              |     X      |      X        |
| Save points                   | X              |     X      |      X        |
| Batching                      | X              |     X      |      X        |
| BLOB/CLOB                     |                |            |               |
| Multiplexed connections       |                |            |               |
| URI-based implement selection |                |            |               |
| Observability                 |                |            |               |
| Transaction isolation         | X              |     X      |      X        |
{:.tablestyle}

# Relational meets Reactive

People wanting to scale while retaining usage of relational databases are cut off from reactive programming due to existing standards. R2DBC introduces a new API that allows asynchronous, non-blocking code that work efficiently with relational databases.

# Cloud Ready

R2DBC supports [cloud native](https://pivotal.io/cloud-native) apps where relational databases like PostgreSQL, MySQL, and others are found. Have the freedom to pick the right one for the job and not be confined by API.

# Community

While led by members of the Spring team at Pivotal, R2DBC depends upon **community support**. Contributors from all relational data stores are invited to participate in building a reactive, relational future.

