---
layout: page
title: Modules
permalink: /modules/
---

R2DBC is comprised of the following modules:

* r2dbc-spi - set of interfaces defining the SPI for R2DBC.
* r2dbc-spi-test - a TCK (Tool Compatibility Kit)

Drivers:

* r2dbc-postgres - driver implemented for PostgreSQL.
* r2dbc-h2 - driver implemented for H2.

Clients:

* r2dbc-client - client implemented on top of the SPI using a Reactor-based solution.
* spring-data-r2dbc - Repository-based Spring Data implementation using R2DBC under the hood.