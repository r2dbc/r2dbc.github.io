---
layout: post
title:  "R2DBC Proxy Tips: Observability"
date:   2021-06-01 18:00:00 -0700
tags: [post]
author: Tadaya Tsuyukubo
---

This is the third post of the _"R2DBC Proxy Tips"_ mini blog series.

This post shows how to achieve observability - metrics and distributed tracing.


To implement observability, we need to capture the interactions with the R2DBC objects.
`ProxyMethodExecutionListener` is suitable for this use case.
This listener is an extension of `ProxyExecutionListener` and provides callbacks for all the methods defined in the R2DBC SPI classes.

For example, the `beforeCreateOnConnectionFactory` method is called back before the `create` method on `ConnectionFactory`.
The `afterExecuteOnStatement` is invoked after the `execute` method on `Statement`.

By using these callback methods, you can easily add logic to populate metrics, start a new span, or take any action you want.

For example, the following listener populates metrics for the time taken to obtain a connection:

```java
public class MyMetricsListener implements ProxyMethodExecutionListener {

	private MeterRegistry registry;

	public MyMetricsListener(MeterRegistry registry) {
		this.registry = registry;
	}

	@Override
	public void beforeCreateOnConnectionFactory(MethodExecutionInfo methodExecInfo) {
		Timer.Sample sample = Timer.start(this.registry);
		methodExecInfo.getValueStore().put("connectionCreate", sample);
	}

	@Override
	public void afterCreateOnConnectionFactory(MethodExecutionInfo methodExecInfo) {
		Timer.Sample sample = methodExecInfo.getValueStore()
				.get("connectionCreate", Timer.Sample.class);

		Timer timer = Timer
				.builder("r2dbc.connection")
				.description("Time to create(acquire) a connection")
				.tags("event", "create")
				.register(this.registry);

		sample.stop(timer);
	}

}
```

As mentioned in the [second post](https://r2dbc.io/2021/05/05/r2dbc-proxy-tips-valuestore), we use the `ValueStore` API to pass the `sample` object between methods.

[MetricsExecutionListener](https://github.com/ttddyy/r2dbc-proxy-examples/blob/master/listener-example/src/main/java/io/r2dbc/examples/MetricsExecutionListener.java) and
[QueryTimeMetricsExecutionListener](https://github.com/ttddyy/r2dbc-proxy-examples/blob/master/listener-example/src/main/java/io/r2dbc/examples/QueryTimeMetricsExecutionListener.java) are other sample metrics listener implementations.


For distributed tracing, the implementation is similar to the above sample code for metrics.
You can create spans at method invocations, pass them to `ValueStore`, and finish them in the appropriate method invocations.

This [TracingExecutionListener](https://github.com/ttddyy/r2dbc-proxy-examples/blob/master/listener-example/src/main/java/io/r2dbc/examples/TracingExecutionListener.java) example shows how to create spans by using the zipkin `Tracer`.

For Spring Cloud Sleuth users, we have good news.
[This commit](https://github.com/spring-cloud/spring-cloud-sleuth/pull/1946) enables out of the box support for R2DBC instrumentation.

