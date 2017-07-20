# Basic

|   layout   |    title   |
|:----------:|:----------:|
|   post     | Elasticsearch使用场景|


## 使用场景

1. 商场在线搜索商品，可以使用Elasticsearch存储商品信息，并提供商品搜索和自动补全建议。  

2. 收集日志和交易数据进行分析和挖掘，以得到数据的趋势、统计等特点。在这种情况下，可以使用Logstash来收集、聚合、转化数据，然后将数据源提供到Elasticsearch，来进行搜索、聚合信息。

3. 制定类目的低价提醒，将类目所有价格导入到Elasticsearch中，并利用其反向搜索能力去匹配价格动向，一旦符合低价则进行提醒。

4. 分析／商业情报需要快速地调查、分析、可视化，并根据大量数据问临时的问题。使用Elasticsearch存储数据，Kibana可视化数据。除此之外，*利用Elasticsearch聚合功能展示复杂的数据情报*。


## 用途

1. 全文检索

主要组成部分

> a. lucene-开源索引引擎，倒排索引

> b. Mapper-attachment-将各种文档比如pdf结构化

> c. Analyzer-分词器明确词界限

2. 文档数据库

主要组成部分

> a. lucene store field-文档数据库

> b. translog-事务日志，可还原内存中丢失的数据

> c. Dynamic-mapping以及schema-free-根据第一次提交的文档自动创建schema, mapping，后面提交的文档需要和该文档类型相同。 

> d. Query DSL

## Refer

[Elasticsearch官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
