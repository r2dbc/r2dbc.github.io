---
layout: default
---

<h2 class="keyvisual">
<img src="images/PVLG-R2DBC-Logo-RGB.png" alt="R2DBC Logo">
</h2>

The Reactive Relational Database Connectivity (R2DBC) project brings reactive programming APIs to relational databases.

# In a Nutshell

**Based on the Reactive Streams specification.** R2DBC is founded on the Reactive Streams specification, which provides a fully-reactive non-blocking API.

**Works with relational databases.** In contrast to the blocking nature of JDBC, R2DBC allows you to work with SQL databases using a reactive API.

**Supports scalable solutions.** With Reactive Streams, R2DBC enables you to move from the classic "one thread per connection" model to a more powerful and scalable approach.

**Provides an open specification.** R2DBC is an open specification and establishes a Service Provider Interface (SPI) for driver vendors to implement and clients to consume.

**Example Query**
 
<ul class="tab_links">
  <li id="tab1"><img src="/images/projectreactor.png" alt="Project Reactor" width="20" /> Project Reactor</li>
  <li id="tab2"><img src="/images/reactivex.png" alt="RxJava" width="20"/> RxJava</li>
  <li id="tab3"><img src="/images/smallrye.png" alt="RxJava" width="20"/> Smallrye Mutiny</li>
</ul>
<div style='clear:both;'></div>
<div class="tab_box" id='home_tab1'>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ConnectionFactory</span> <span class="n">connectionFactory</span> <span class="o">=</span> <span class="n">ConnectionFactories</span>
  <span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"r2dbc:h2:mem:///testdb"</span><span class="o">);</span>

<span class="n">Mono</span><span class="o">.</span><span class="na">from</span><span class="o">(</span><span class="n">connectionFactory</span><span class="o">.</span><span class="na">create</span><span class="o">())</span>
  <span class="o">.</span><span class="na">flatMapMany</span><span class="o">(</span><span class="n">connection</span> <span class="o">-&gt;</span> <span class="n">connection</span>
    <span class="o">.</span><span class="na">createStatement</span><span class="o">(</span><span class="s">"SELECT firstname FROM PERSON WHERE age &gt; $1"</span><span class="o">)</span>
    <span class="o">.</span><span class="na">bind</span><span class="o">(</span><span class="s">"$1"</span><span class="o">,</span> <span class="mi">42</span><span class="o">)</span>
    <span class="o">.</span><span class="na">execute</span><span class="o">())</span>
  <span class="o">.</span><span class="na">flatMap</span><span class="o">(</span><span class="n">result</span> <span class="o">-&gt;</span> <span class="n">result</span>
    <span class="o">.</span><span class="na">map</span><span class="o">((</span><span class="n">row</span><span class="o">,</span> <span class="n">rowMetadata</span><span class="o">)</span> <span class="o">-&gt;</span> <span class="n">row</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"firstname"</span><span class="o">,</span> <span class="n">String</span><span class="o">.</span><span class="na">class</span><span class="o">)))</span>
  <span class="o">.</span><span class="na">doOnNext</span><span class="o">(</span><span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">::</span><span class="n">println</span><span class="o">)</span>
  <span class="o">.</span><span class="na">subscribe</span><span class="o">();</span>
</code></pre></div></div>
</div>
<div class="tab_box" id='home_tab2'>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ConnectionFactory</span> <span class="n">connectionFactory</span> <span class="o">=</span> <span class="n">ConnectionFactories</span>
  <span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"r2dbc:h2:mem:///testdb"</span><span class="o">);</span>

<span class="n">Single</span><span class="o">.</span><span class="na">fromPublisher</span><span class="o">(</span><span class="n">connectionFactory</span><span class="o">.</span><span class="na">create</span><span class="o">()).</span><span class="na">toFlowable</span><span class="o">()</span>
  <span class="o">.</span><span class="na">flatMap</span><span class="o">(</span><span class="n">connection</span> <span class="o">-&gt;</span> <span class="n">connection</span>
    <span class="o">.</span><span class="na">createStatement</span><span class="o">(</span><span class="s">"SELECT firstname FROM PERSON WHERE age &gt; $1"</span><span class="o">)</span>
    <span class="o">.</span><span class="na">bind</span><span class="o">(</span><span class="s">"$1"</span><span class="o">,</span> <span class="mi">42</span><span class="o">)</span>
    <span class="o">.</span><span class="na">execute</span><span class="o">())</span>
  <span class="o">.</span><span class="na">flatMap</span><span class="o">(</span><span class="n">result</span> <span class="o">-&gt;</span> <span class="n">result</span>
    <span class="o">.</span><span class="na">map</span><span class="o">((</span><span class="n">row</span><span class="o">,</span> <span class="n">rowMetadata</span><span class="o">)</span> <span class="o">-&gt;</span> <span class="n">row</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"firstname"</span><span class="o">,</span> <span class="n">String</span><span class="o">.</span><span class="na">class</span><span class="o">)))</span>
  <span class="o">.</span><span class="na">doOnNext</span><span class="o">(</span><span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">::</span><span class="n">println</span><span class="o">)</span>
  <span class="o">.</span><span class="na">subscribe</span><span class="o">();</span>
</code></pre></div></div>
</div>
<div class="tab_box" id='home_tab3'>
<div class="language-java highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ConnectionFactory</span> <span class="n">connectionFactory</span> <span class="o">=</span> <span class="n">ConnectionFactories</span>
  <span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"r2dbc:h2:mem:///testdb"</span><span class="o">);</span>

<span class="nc">Uni</span><span class="o">.</span><span class="na">createFrom</span><span class="o">().</span><span class="na">publisher</span><span class="o">(</span><span class="n">connectionFactory</span><span class="o">.</span><span class="na">create</span><span class="o">())</span>
  <span class="o">.</span><span class="na">onItem</span><span class="o">().</span><span class="na">transformToMulti</span><span class="o">(</span><span class="n">connection</span> <span class="o">-&gt;</span> <span class="n">connection</span>
    <span class="o">.</span><span class="na">createStatement</span><span class="o">(</span><span class="s">"SELECT firstname FROM PERSON WHERE age &gt; $1"</span><span class="o">)</span>
    <span class="o">.</span><span class="na">bind</span><span class="o">(</span><span class="s">"$1"</span><span class="o">,</span> <span class="mi">42</span><span class="o">)</span>
    <span class="o">.</span><span class="na">execute</span><span class="o">())</span>
  <span class="o">.</span><span class="na">onItem</span><span class="o">().</span><span class="na">transform</span><span class="o">(</span><span class="n">result</span> <span class="o">-&gt;</span> <span class="n">result</span>
    <span class="o">.</span><span class="na">map</span><span class="o">((</span><span class="n">row</span><span class="o">,</span> <span class="n">rowMetadata</span><span class="o">)</span> <span class="o">-&gt;</span> <span class="n">row</span><span class="o">.</span><span class="na">get</span><span class="o">(</span><span class="s">"firstname"</span><span class="o">,</span> <span class="nc">String</span><span class="o">.</span><span class="na">class</span><span class="o">)))</span>
  <span class="o">.</span><span class="na">subscribe</span><span class="o">().</span><span class="na">with</span><span class="o">(</span><span class="nc">System</span><span class="o">.</span><span class="na">out</span><span class="o">::</span><span class="n">println</span><span class="o">);</span>
</code></pre></div></div>
</div>

# Features

* [Broad type conversion](/spec/0.8.3.RELEASE/spec/html/#datatypes)
* [Transactions, isolation levels, and save points](/spec/0.8.3.RELEASE/spec/html/#transactions)
* [Batching](/spec/0.8.3.RELEASE/spec/html/#batches)
* [BLOB/CLOB support](/spec/0.8.3.RELEASE/spec/html/#datatypes.mapping.advanced)
* [Connection URLs](/spec/0.8.3.RELEASE/spec/html/#overview.connection.url) (`r2dbc:<driver>://<host>:<port>/<database>`)
* `ConnectionFactory` discovery and configuration based on Java's `ServiceLoader`
* [Typed Exceptions](/spec/0.8.3.RELEASE/spec/html/#exceptions)
* [Extensible Interface](/spec/0.8.3.RELEASE/spec/html/#extensions)
* [Observability](https://github.com/r2dbc/r2dbc-proxy/)
* [TCK](/spec/0.8.3.RELEASE/spec/html/#compliance)

# Relational Meets Reactive

Existing standards, based on blocking I/O, cut off reactive programming from relational database users. R2DBC specifies a new API to allow reactive code that works efficiently with relational databases.

R2DBC is a specification designed from the ground up for reactive programming with SQL databases. It defines a non-blocking SPI for database driver implementors and client library authors. R2DBC drivers fully implement the database wire protocol on top of a non-blocking I/O layer.

# Design Principles

R2DBC aims for a minimal SPI surface, specifying only parts that differ across databases, and is fully reactive and backpressure-aware all the way down to the database. It is intended primarily as a driver SPI to be consumed by client libraries and not intended to be used directly in application code.

# Cloud Ready

R2DBC supports cloud-native applications using relational databases such as PostgreSQL, MySQL, and others. Application developers are free to pick the right database for the job without being confined by APIs.

# Community

Join the [R2DBC Community Forum](https://groups.google.com/g/r2dbc) to learn more about R2DBC, get your R2DBC questions answered, and interact with other R2DBC developers.

<script src="https://code.jquery.com/jquery-1.11.3.min.js"></script>
<script>
function hideOtherTabs(tabList, tab, tabPrefix){
	
	for	(index = 0; index < tabList.length; index++) {
		if(tabPrefix+tab!=tabPrefix+tabList[index]){
			$('div#'+tabPrefix+tabList[index]).hide();
		}
	}
}

$(document).ready( function(){
 
	var tabPrefix = 'home_';
	var tabs = ['tab1', 'tab2', 'tab3'];
	
	for	(index = 1; index < tabs.length; index++) {
		jQuery('div#'+tabPrefix+tabs[index]).hide();
	}
		
	$('ul.tab_links li').click( function(){
		 
		var tabID = $(this).attr('id');
		//show this tab
		$('div#'+tabPrefix+tabID).show();
		
		//hide others
		hideOtherTabs(tabs,tabID,tabPrefix);
	});
});
</script>