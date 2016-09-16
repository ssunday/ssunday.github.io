---
layout: post
title: ElasticSearch Queries
description: using the goldenhammer for querying
date: 16/9/2016
category: "ElasticSearch"
---

[Elasticsearch is a tool for searching.](https://www.elastic.co/products/elasticsearch) Elastic being a part of its name, it is rather flexible. Whatever you need to search on and how, it can probably do.

Say you wanted to do an exact match on a value or any value of an array of values to a particular type's properties. You would use a term query. If the field you are doing the query on is `score` and you want results returning `10` you would make a term query of:

```ElasticSearch

{
    "term" :
	{
		"score" : 10
	}
}
```

This would do an exact match of scores to the *integer* 10, giving back all the results of your index where the score is 10. This query, using `terms`, on the other hand, would return matches on 10 or 20:

```ElasticSearch

{
    "terms" :
	{
		"score" : [10, 20]
	}
}
```

But if the score was typed as an string in the index's mapping, these queries might not work and you'd get back nothing.

Yes, ElasticSearch *does* have typing. It exists in a map for the index. You don't have to define the mapping of all the properties of your types. Elasticsearch is intelligent and infers them from the documents present in that type. There might be cases for when you want to explicitly define the type for a field. Such as with strings.

Why strings? Because ElasticSearch does something a little different for them. [To do match queries or full text queries on a field, Elasticsearch runs the strings through an analyzer at indexing time, basically tokenizing the strings into bits and pieces for it to match on.](https://www.elastic.co/guide/en/elasticsearch/guide/current/analysis-intro.html) This is all well and good if you are running full-text queries on that field, but if you are trying to do a term query on an analyzed string, then you're going to have a hard time. Since the string has been analyzed, doing an exact match of `This is My Value` to the field isn't going to return anythign because the value of the field has been tokenized into a bunch of substring like `this` `is` `my` `value` or something like that. So it isn't going to match.

And this is where making explicit typing is important depending on the particular use case. If you know you want to do a term query on a string field, you can disable the analyzer from tokenizing it by specifying from that field to be not analyzed in your mapping, like this:

``` ElasticSearch
"mappings": {
    "student": {
      "properties": {
	    "id" : {
			"type" : "integer"
		},
		"name": {
			"type" : "string"
		},
        "email": {
			"type" : "string",
			"index" : "not_analyzed"
		},
        "score": {
			"type" : "integer"
		}
      }
    }
}
```

So when you do a full index with this mapping, you will be able to do a term query with the `name` property. It has to be a full re-index because it can't easily undo a tokenization it already did. Which can take a while depending on the data and your particular indexing process, so really think through the type of query you are going to use and what fields needed prior to indexing the first time.

There are other query types, along with many subqueries. Term query has range queries, exists, missing, and a few others. They can be strung together within the greater query.

The greater query, `query` is usually contained with a `bool` block that has different contexts such as filter or must which control whether ElasticSearch will do any scoring on your results--basically trying to figure out how well the results match the query. Filter is basically like "give me what matches this" and must queries actually add to the scoring.

Example query:

``` ElasticSearch
"query": {
    "bool": {
	  "must": [
	    {
			"match": {
				"name": "Search"
			}
	    }
		]
      "filter": [
        {
			"term" : {
				"score" : 10
			}
		}
		]
	}
}
```

Filters and musts can have multiple `term`'s or `match`'s or whatever you are querying on.

ElasticSearch queries are highly composable. Basically you can search on whatever you need to search on--it has so many tools for you to use. The only pitfall is that there are many nuances to Elasticsearch that may not seem obvious, such as the string analyzer and what mapping means for searching. [But the good thing with ElasticSearch is that the documentation is that the documentation is actually well-written and helpful.](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) Surprise! You don't have to search around for blog posts to illuminate what it is doing. Elastic does a very good job of that themselves and doesn't skimp on providing examples of queries and pointing out some of the nuances.

There is complexity to ElasticSearch, but it isn't a daunting complexity. It is a complexity that gives power to the wielder of this great goldenhammer. Use it wisely.
