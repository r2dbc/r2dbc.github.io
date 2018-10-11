---
layout: page
title: Modules
permalink: /modules/
---

R2DBC is comprised of several official modules.

First and foremost, is the **Service Provider Interface (SPI)**:

* [r2dbc-spi](https://github.com/r2dbc/r2dbc-spi) - set of interfaces defining the SPI for R2DBC
* [r2dbc-spi-test](https://github.com/r2dbc/r2dbc-spi/tree/master/r2dbc-spi-test) - a **Test Compatibility Kit (TCK)** contained with the SPI repository for verifying your implementation of the SPI.

Drivers:

* [r2dbc-postgres](https://github.com/r2dbc/r2dbc-postgresql) - driver implemented for PostgreSQL.
* [r2dbc-h2](https://github.com/r2dbc/r2dbc-h2) - driver implemented for H2.

Clients:

* [r2dbc-client](https://github.com/r2dbc/r2dbc-client) - client implemented on top of the SPI using pure Reactor (i.e. no Spring dependencies).
* spring-data-r2dbc - Repository-based Spring Data implementation using R2DBC under the hood.
