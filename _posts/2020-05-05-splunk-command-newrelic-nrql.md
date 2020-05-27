---
layout: post
title: "New Relic NRQL Command for Splunk"
description: "Execute NRQL statements to query New Relic data from Splunk at no extra cost."
image: "/assets/images/p201.jpg"
---
<img class="w-100" src="{{ page.image }}" alt="{{ page.title }}">

[Splunk](https://www.splunk.com){:target="_blank"} and [New Relic](https://newrelic.com/){:target="_blank"} are the most popular Observability platforms. Splunk is a powerful operational intelligence & log monitoring tool. New Relic product suite includes Application Performance Monitoring (APM), Real User Monitoring (Browser), Synthetics, Mobile, Infrastructure, and a lot more.

Similar to Splunk SPL ([Search Processing Language](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/WhatsInThisManual){:target="_blank"}), New Relic provides NRQL ([New Relic Query Language](https://docs.newrelic.com/docs/query-data/nrql-new-relic-query-language/getting-started/introduction-nrql){:target="_blank"}) to query the data and visualize in New Relic One & New Relic Insights. 

Example SPL: `index=main | stats count` <br/>Example NRQL: `select count(*) from PageView`

The Splunk [Add-on](https://splunkbase.splunk.com/app/3465/){:target="_blank"} and [App](https://splunkbase.splunk.com/app/3466/){:target="_blank"} for New Relic in Splunkbase delivers what it promises. However, the add-on collects data from New Relic and indexes it in Splunk, which adds to the Splunk license and storage. 

Have you ever thought about executing NRQL statements to query New Relic data in Splunk at no extra cost, the same way you run ad-hoc queries to remote databases using `dbxquery` command?

[New Relic NRQL Command for Splunk](https://splunkbase.splunk.com/app/4988/){:target="_blank"} is the answer to your question. This app contains Splunk Generating Command `nrql` which queries New Relic and generates Splunk reports from the query results returned.

Syntax:<br/>
`| nrql connection=<string> query=<string> (output=_raw)?`

Example 1:<br/>
<code>
| nrql connection="example-account" query="select count(*) from PageView since yesterday"
</code>
<br/>
<img class="w-100" src="/assets/images/p202.png" alt="nrql">

Example 2:<br/>
<code>
| nrql connection="example-account" query="select count(*) from PageView since yesterday facet deviceType" 
| table deviceType, count
</code>
<br/>
<img class="w-100" src="/assets/images/p203.png" alt="nrql">

Example 3:<br/>
<code>
| nrql connection="example-account" query="select count(*) from PageView 
since '2020-05-03 00:00:00' until '2020-05-04 00:00:00' 
facet deviceType timeseries auto" 
| eval _time=strptime(beginTimeSeconds,"%s")
| xyseries _time, deviceType, count
</code>
<br/>
<img class="w-100" src="/assets/images/p204.png" alt="nrql">

Download the app today from Splunkbase: [https://splunkbase.splunk.com/app/4988/](https://splunkbase.splunk.com/app/4988/){:target="_blank"}

Would you like to try this app on a Splunk sandbox before deploying it on a production search head? Try [Splunk Sandbox The Easy Way](/docker-splunk-minion.html).

For documentation and source code, please see [https://github.com/dmanojbaba/splunk-command-newrelic-nrql](https://github.com/dmanojbaba/splunk-command-newrelic-nrql){:target="_blank"}

---