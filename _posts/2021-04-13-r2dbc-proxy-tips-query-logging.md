---
layout: post
title:  "R2DBC Proxy Tips: Query Logging"
date:   2021-04-13 18:00:00 -0700
tags: [post]
author: Tadaya Tsuyukubo
---

[R2DBC Proxy](https://github.com/r2dbc/r2dbc-proxy) is a framework that provides callbacks to the R2DBC interactions.
It consists of a thin layer on top of the R2DBC drivers to implement cross-cutting concerns, such as query loggings, observability instrumentation, or your own actions.

_R2DBC Proxy Tips_ is a series of mini blog posts.
I will introduce typical usage of the R2DBC proxy and sample implementations with tips.

This first post explains the prime use case of the R2DBC Proxy: _"how to log queries"_.


## Implementation

In R2DBC Proxy, a callback is implemented as `ProxyExecutionListener`.

This listener interface defines `beforeQuery` and `afterQuery` callback methods.
As the names suggest, they are invoked when queries get executed.

To log the executed queries, you can create a listener that performs logging in `beforeQuery` or `afterQuery`. (Note, some of the values, such as the time the query took to run, are available only on the `afterQuery`.)


The following example shows a listener implementation that logs queries after each query:

```java
public class LoggingListener implements ProxyExecutionListener {

  private static final Logger logger = LoggerFactory.getLogger(LoggingListener.class);

  private final QueryExecutionInfoFormatter formatter = QueryExecutionInfoFormatter.showAll();

  @Override
  public void afterQuery(QueryExecutionInfo execInfo) {
    logger.info(this.formatter.format(execInfo));
  }

}
```

Instead of creating a dedicated `LoggingListener` class, you can also register a listener for this purpose while creating a proxy `ConnectionFactory`.

```java
QueryExecutionInfoFormatter formatter = QueryExecutionInfoFormatter.showAll();

ConnectionFactory original = ...;

// create a proxy ConnectionFactory
ConnectionFactory connectionFactory = ProxyConnectionFactory.builder(original)
    .onAfterQuery(queryInfo -> {  // listener
        logger.info(formatter.format(queryInfo));
    })
    .build();
```


Sample Output (multiline for display purpose)
```
Thread:http-nio-8080-exec-3(38) Connection:3 Transaction:{Create:1 Rollback:0 Commit:0}
Success:True Time:5 Type:Statement BatchSize:0 BindingsSize:1
Query:["INSERT INTO test VALUES ($1)"] Bindings:[($1=100)]
```

## Customizing a Formatter

`QueryExecutionInfoFormatter` is a utility class that converts `QueryExecutionInfo` to a `String` for logging.
The default static method, `showAll()`, creates a formatter that converts all information available in the query execution.

However, it may be too long for your logging or you may want to customize the format.

`QueryExecutionInfoFormatter` provides `show...` methods to selectively choose the information you want to include, or you can use `addConsumer` to add your own conversion logic.
The following example uses `showQuery()` and `showBinding()` with new lines for nicer formatting:

```java
QueryExecutionInfoFormatter custom = new QueryExecutionInfoFormatter()
    .addConsumer((info, sb) -> {
      // custom conversion
      sb.append("ConnID=");
      sb.append(info.getConnectionInfo().getConnectionId());
    })
    .newLine()
    .showQuery()
    .newLine()
    .showBindings()
    .newLine();
```

Sample output:
```
ConnID=1
Query:["SELECT * FROM employee WHERE id=$1"]
Bindings:[($1=200)]
```
