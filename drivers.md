---
layout: page
title: Drivers
permalink: /drivers/
---

This section is dedicated toward writing an R2DBC driver for database.

## Service Provider Interface (SPI)

R2DBC has a clearly defined **SPI** you must implement to host a solution for your data store. To build an implementation, you need the following artifact added to your build:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi**

## Test Compatibility Kit (TCK)

R2DBC also has a suite of test cases to verify your support. Your data store implementation is expected to import a test-scoped dependency on:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi-test**

To run all the tests that are expected, write a test class like this:

```java
/**
 * Your class must extend R2DBC SPI Test's Example class.
 *
 * The generic type for Example is however you transform a binding query param into column notation,
 * e.g. "$1" => "0" would be String while "$1" => 0 (an int) would be Integer.
 */
final class PostgresqlExample implements Example<String> {

	/**
	 * A JUnit 5-based extension to spin up a test database, 
	 * whether using some dockerized apprpoach or an embeddable
	 * instance if possible.
	 */
    @RegisterExtension
    static final PostgresqlServerExtension SERVER = new PostgresqlServerExtension();

    /**
     * Whatever is needed to put together a connection to SERVER.
     */
    private final PostgresqlConnectionConfiguration configuration = PostgresqlConnectionConfiguration.builder()
        .database(SERVER.getDatabase())
        .host(SERVER.getHost())
        .port(SERVER.getPort())
        .password(SERVER.getPassword())
        .username(SERVER.getUsername())
        .build();

    private final PostgresqlConnectionFactory connectionFactory = new PostgresqlConnectionFactory(this.configuration);

    /**
     * The SPI needs an R2DBC ConnectionFactory instance to create a connection and run tests.
     */
    @Override
    public PostgresqlConnectionFactory getConnectionFactory() {
        return this.connectionFactory;
    }

    /**
     * For binding insert statements, convert a column number into a column identifier.
     * 
     * e.g. Column 0 => "$1"
     */
    @Override
    public String getIdentifier(int index) {
        return getPlaceholder(index);
    }

    /**
     * For before/after, R2DBC SPI Test leverages Spring's JdbcTemplate for setup and teardown.
     */
    @Override
    public JdbcOperations getJdbcOperations() {
        JdbcOperations jdbcOperations = SERVER.getJdbcOperations();

        if (jdbcOperations == null) {
            throw new IllegalStateException("JdbcOperations not yet initialized");
        }

        return jdbcOperations;
    }

    /**
     * For actualy query construction, convert a column index into a placeholder.
     * 
     * e.g. Column 0 => "$1"
     */
    @Override
    public String getPlaceholder(int index) {
        return String.format("$%d", index + 1);
    }
}
```

See [r2dbc-postgresql's Example](https://github.com/r2dbc/r2dbc-postgresql/blob/master/src/test/java/io/r2dbc/postgresql/PostgresqlExample.java) to read the full source.