---
layout: page
title: Resources
permalink: /resources/
---

R2DBC is comprised of several official projects along with examples and presentations.

# Service Provider Interface (SPI)

R2DBC defines an SPI all data store drivers must implement.

* [r2dbc-spi](https://github.com/r2dbc/r2dbc-spi) - set of interfaces defining the SPI for R2DBC.
* [r2dbc-spi-test](https://github.com/r2dbc/r2dbc-spi/tree/master/r2dbc-spi-test) - a **Technology Compatibility Kit (TCK)** contained within the SPI repository for verifying your driver's implementation.

One noticeable difference between R2DBC and JDBC is that JDBC is aimed at both driver writers as well as application developers. Drivers and applications operate on different levels, making this one-size-fits-all less than ideal.

R2DBC's SPI is deliberately designed to be as small as possible while still capturing critical features for ANY relational data store. This means that data store specific extensions are not targeted by the SPI.

And to ease implementation, a test interface, a veritable TCK, is provided to ensure you are fully operational.

# Drivers

R2DBC drivers implements the SPI listed above. The ones currently supported include:

* [r2dbc-postgres](https://github.com/r2dbc/r2dbc-postgresql) - driver implemented for PostgreSQL.
* [r2dbc-h2](https://github.com/r2dbc/r2dbc-h2) - driver implemented for H2 as a test database.

# Clients

As mentioned earlier, clients and drivers do NOT have to leverage the same interfaces (compared to JDBC). The following list gives you options to build an app using R2DBC:

* [r2dbc-client](https://github.com/r2dbc/r2dbc-client) - client implemented on top of the SPI using pure Reactor (i.e. no Spring dependencies).
* spring-data-r2dbc - Repository-based Spring Data implementation using R2DBC under the hood.

These clients can also serve as inspiration if you wish to code your own client.

# Videos

Here is a series of videos related to R2DBC.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/tciPoh1vmmY" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# Other resources

* [r2dbc.github.io](https://github.com/r2dbc/r2dbc.github.io) - this site.
