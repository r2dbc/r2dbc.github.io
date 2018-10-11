---
layout: page
title: Drivers
permalink: /drivers/
---

This section is dedicated toward writing an R2DBC driver for database.

# Service Provider Interface (SPI)

R2DBC has a clearly defined **SPI** you must implement to host a solution for your data store. To build an implementation, add the following artifact to your build:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi**

The key interface all driver providers must implements is the `Connection` as shown below:

```
Publisher<Void> beginTransaction();
Publisher<Void> close();
Publisher<Void> commitTransaction();
Batch createBatch();
Publisher<Void> createSavepoint(String name);
Statement createStatement(String sql);
Publisher<Void> releaseSavepoint(String name);
Publisher<Void> rollbackTransaction();
Publisher<Void> rollbackTransactionToSavepoint(String name);
Publisher<Void> setTransactionIsolationLevel(IsolationLevel level);
```

There are other parts to implement, but this is the core.

# Technology Compatibility Kit (TCK)

R2DBC also has a suite of test cases to verify your support. Your data store implementation should import a test-scoped dependency on:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi-test**

To run all the tests that are expected, write an implementation of the TCK's `Example<T>` test class like this:

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
     * whether using some dockerized approach or an embeddable
     * instance if possible.
     */
    @RegisterExtension
    static final PostgresqlServerExtension SERVER = new PostgresqlServerExtension();

    /**
     * Links the test database connection details to the SPI's ConnectionConfiguration.
     */
    private final PostgresqlConnectionConfiguration configuration = PostgresqlConnectionConfiguration.builder()
        .database(SERVER.getDatabase())
        .host(SERVER.getHost())
        .port(SERVER.getPort())
        .password(SERVER.getPassword())
        .username(SERVER.getUsername())
        .build();

    /**
     *  Using the configuration details, create a ConnectionFactory.
     */
    private final PostgresqlConnectionFactory connectionFactory = new PostgresqlConnectionFactory(this.configuration);

    /**
     * The TCK needs a ConnectionFactory to create a connection and run all of its tests.
     */
    @Override
    public PostgresqlConnectionFactory getConnectionFactory() {
        return this.connectionFactory;
    }

    /**
     * For binding insert statements, convert a column number into a column identifier.
     * 
     * e.g. Column 0 => "$1" (PostgreSQL's notation)
     */
    @Override
    public String getIdentifier(int index) {
        return getPlaceholder(index);
    }

    /**
     * For before/after, the TCK leverages Spring's JdbcTemplate for setup and teardown.
     * NOTE: R2DBC uses Spring for test purposes only. It's NOT required in either the SPI itself,
     *       or for driver implementations.
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
     * For SQL construction, convert a column index into a placeholder.
     * 
     * e.g. Column 0 => "$1" (PostgreSQL's notation)
     */
    @Override
    public String getPlaceholder(int index) {
        return String.format("$%d", index + 1);
    }
}
```

See [r2dbc-postgresql's Example](https://github.com/r2dbc/r2dbc-postgresql/blob/master/src/test/java/io/r2dbc/postgresql/PostgresqlExample.java) to read the full source.