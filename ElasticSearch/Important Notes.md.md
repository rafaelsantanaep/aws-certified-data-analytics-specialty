#### Elasticsearch


##### Operation Intelligence

**Wikipedia Definition**:
Operational intelligence (OI) is a category of real-time dynamic, business analytics that delivers visibility and insight into data, streaming events and business operations. OI solutions run queries against streaming data feeds and event data to deliver analytic results as operational instructions. OI provides organizations the ability to make decisions and immediately act on these analytic insights, through manual or automated actions.


**AWS Definition**:
Operational intelligence refers to a set of technologies that can extract useful knowledge from a variety of data sources, in a dynamic and real-time fashion, to help organizations make decisions.

**Use Cases**:
-   Application Performance Monitoring (APM)
-   Log Analytics
-   Full-Text Search (Google-like search)
-   Clickstream Analytics
-   Security Analytics

#### Kibana

##### Import and Export dashboards
**Justification**:

Kibana is a popular open-source visualization tool designed to work with Elasticsearch. [Amazon Elasticsearch Service](https://aws.amazon.com/elasticsearch-service/) (Amazon ES) provides an installation of Kibana with every Amazon ES domain. Users of Kibana can create visualizations and add them into a [dashboard](https://aws.amazon.com/blogs/database/configuring-and-authoring-kibana-dashboards/). As organizations invest time and resources into creating these dashboards, the need arises to reuse these dashboards within additional Amazon ES domains or even in additional AWS accounts.

A dashboard can be exported using the Web UI or the Rest API. The output of this operation is a NDJSON file that can be used to import a dashboard in another Kibana.

