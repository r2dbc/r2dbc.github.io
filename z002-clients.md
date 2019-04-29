---
layout: page
title: Clients
permalink: /clients/
---

R2DBC encourages app writers to have access to a "humane" API. There is no need to be tied to the same exact same API as driver authors.

If you're eager to start using R2DBC to build an application, check out the [existing clients](#existing-clients) listed below. If you're interested in crafting your own client, check out the section on [new clients](#new-clients) further down.

## Existing clients

TODO: Eventually include links to documentation for the following clients.

* [r2dbc-client](https://github.com/r2dbc/r2dbc-client) - client using pure Reactor (i.e. no Spring dependencies).
* [spring-data-r2dbc](https://github.com/spring-projects/spring-data-r2dbc) - Spring Data client for R2DBC.

## New clients

R2DBC's minimal SPI makes it easy to write a custom client. The modules above can provide inspiration if you wish to write a different client for the community.

To write a custom client, R2DBC's `Connection` SPI provides you the necessary building blocks:

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

TODO: More documentation links per client development.

The SPI can be found at:

* Group: **io.r2dbc**
* Artifact: **r2dbc-spi**

This artifact contains R2DBC's `Connection` interface (and others) which you can wrap up inside your custom client.

### Testing your client

To test your client, you are encouraged to utilize the following components in a test-scoped fashion:

* `io.projectreactor:reactor-test` - Reactor's test utilities.
* `org.junit.jupiter:junit-jupiter-api` and `org.junit.jupiter:junit-jupiter-engine` - JUnit 5 basics.
* `io.r2dbc:r2dbc-h2` - In-memory test database driver your client can use.
* `org.springframework.boot:spring-boot-starter-jdbc` - set up and tear down the database using `JdbcTemplate`.

Using Spring + H2, it's very easy to spin up a test database, prepopulate it with tables and data, and then tear things down afterward.

First, create a shell of a test suite by creating the following JUnit 5 test class:

```java
final class MyCoolR2dbcClient {

    @RegisterExtension
    static final H2ServerExtension SERVER = new H2ServerExtension();

    private final H2ConnectionConfiguration configuration = H2ConnectionConfiguration.builder()
        .database(SERVER.getDatabase())
        .password(SERVER.getPassword())
        .url(SERVER.getUrl())
        .username(SERVER.getUsername())
        .build();

    private final H2ConnectionFactory connectionFactory = new H2ConnectionFactory(this.configuration);

    // Test cases coming soon!
}
```

Next add a static inner class to connect to H2:

```java
private static final class H2ServerExtension implements BeforeAllCallback, AfterAllCallback {

	@Override
	public void beforeAll(ExtensionContext context) throws Exception {
	    this.dataSource = DataSourceBuilder.create()
	        .type(HikariDataSource.class)
	        .url(String.format("jdbc:h2:%s:%s;USER=%s;PASSWORD=%s;DB_CLOSE_DELAY=-1;TRACE_LEVEL_FILE=4", this.url, this.database, this.username, this.password))
	        .build();

	    this.dataSource.setMaximumPoolSize(1);

	    this.jdbcOperations = new JdbcTemplate(this.dataSource);
	}

	@Override
	public void afterAll(ExtensionContext context) {
	    this.dataSource.close();
	}
}
```

JUnit 5's `BeforeAllCallback` gives you a hook to connect to your test database. The `AfterAllCallback` interface gives you the hook to tear things down afterward.

Assuming you flesh out the rest of your extension, you can now write test cases like this:

```java
@Test
public void testSomeScenario() {
	SERVER.getJdbcOperations.execute("CREATE TABLE blah (blah blah)");

	// Test some aspect of your client here

	SERVER.getJdbcOperations.execute("DROP TABLE blah");
}
```



