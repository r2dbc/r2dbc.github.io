---
layout: post
title:  "R2DBC Proxy Tips: Share values in callbacks with ValueStore"
date:   2021-05-04 18:00:00 -0700
tags: [post]
author: Tadaya Tsuyukubo
---

[R2DBC Proxy](https://github.com/r2dbc/r2dbc-proxy) is a framework that provides callbacks to the R2DBC interactions.
It consists of a thin layer on top of the R2DBC drivers to implement cross-cutting concerns, such as query loggings, observability instrumentation, or your own actions.

_R2DBC Proxy Tips_ is a series of mini blog posts.
I will introduce typical usage of the R2DBC proxy and sample implementations with tips.


# Share values in callbacks with ValueStore

This is the second post of the _"R2DBC Proxy Tips"_ mini blog series.

This post shows how to pass values across proxy callbacks.

When you implement a `ProxyExecutionListener`, you may want to pass values from the `beforeQuery` to the `afterQuery` callback, pass values from the `beforeMethod` to the `afterMethod` callback, or bind to `Connection` scope and share across multiple callbacks.

In imperative programming, `ThreadLocal` provides the functionality to pass values between methods or keep values bound to a database connection. However, in reactive, `ThreadLocal` is not a reliable place to store values.

To address this, R2DBC Proxy provides `ValueStore`. This provides a `Map`-like API to put and get objects by key.
`ValueStore` is available for the following scopes:

- Between `beforeMethod` and `afterMethod` through `MethodExecutionInfo`
- Between `beforeQuery` and `afterQuery` through `QueryExecutionInfo`
- `Connection` bound through `ConnectionInfo`
- `Statement` bound through `StatementInfo` for the bind parameter converter


The following hypothetical usage shows how to put or get values to or from `Connection` and method-bound `ValueStore` instances.

```java
static class MyFilter implements ProxyMethodExecutionListener {

  private static final Logger log = LoggerFactory.getLogger(MyFilter.class);

  private final Clock clock;

  public MyFilter(Clock clock) {
    this.clock = clock;
  }

  @Override
  public void afterCreateOnConnectionFactory(MethodExecutionInfo methodInfo) {
    // connection scoped store
    ValueStore store = methodInfo.getConnectionInfo().getValueStore();
    store.put("conn-created", this.clock.instant());
  }

  @Override
  public void beforeExecuteOnStatement(MethodExecutionInfo methodInfo) {
    // method scoped store
    ValueStore store = methodInfo.getValueStore();
    store.put("stmt-before", this.clock.instant());
  }

  @Override
  public void afterExecuteOnStatement(MethodExecutionInfo methodInfo) {
    ValueStore connectionStore = methodInfo.getConnectionInfo().getValueStore();
    ValueStore methodStore = methodInfo.getValueStore();

    Instant connCreated = connectionStore.get("conn-created", Instant.class);
    Instant stmtBefore = methodStore.get("stmt-before", Instant.class);

    Instant now = this.clock.instant();
    Duration connToNow = Duration.between(connCreated, now);
    Duration stmtToNow = Duration.between(stmtBefore, now);

    log.info("From connection created={}", connToNow);
    log.info("From statement executed={}", stmtToNow);
  }

}
```

The next blog post will show how to implement a listener for metrics and distributed tracing.

The `ValueStore` is used to keep the current metrics and span information.

