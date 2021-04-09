"SANDBOX" for Testing Elasticsearch( - show how curl requests are processed )
=============================================================================

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html>

<https://hub.docker.com/_/elasticsearch/?ref=login>

Now(`9.04.2021`), current versions of `Elasticsearch`( `7.12.0` OR `6.8.15` ).

---

[Live Coding School - ElasticSearch	( 1-4 videos ~32 min. )]( https://www.youtube.com/watch?v=qDt70R4i3wk&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&ab_channel=LiveCodingSchool )

[1 ElasticSearch что это такое - ElasticSearch уроки (8:45)]( https://www.youtube.com/watch?v=qDt70R4i3wk&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&ab_channel=LiveCodingSchool )

[(5:35)]( https://youtu.be/qDt70R4i3wk?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=335 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1lcs/4.png )

`In Terminal:`

	docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.12.0
	
OR	

	docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.8.15

`In another Terminal:`

	curl -X GET "localhost:9200"
	curl -X GET "localhost:9200/_cat/nodes?v=true&pretty"
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/1.png )

INSTALL POSTMAN for Firefox:

<https://linuxthebest.net/kak-ustanovit-portman-v-ubuntu-16-04-18-04/>

	sudo snap install postman

---

[3 ElasticSearch пример использования запросы - ElasticSearch уроки]( https://www.youtube.com/watch?v=Dg5pztsa80c&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&index=3&ab_channel=LiveCodingSchool )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/3lcs/3.png )

[(0:40)]( https://youtu.be/Dg5pztsa80c?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=40 )

`In Terminal:`

```
curl -X PUT "localhost:9200/test_index/_doc/1"
{
	"title": "Fighting Ebola with Elastic",
	"category": "User Stories",
	"author": {
	"first_name": "Emily",
	"last_name": "Mother"
	}
}
```

Error:

_Content-type header not supported_

<https://stackoverflow.com/questions/51378099/content-type-header-not-supported> 

```
curl -X PUT -H accept:application/json -H Content-type:application/json --data-binary '{ "title": "Fighting Ebola with Elastic", "category": "User Stories", "author": { "first_name": "Emily", "last_name": "Mother"} }' "localhost:9200/test_index/_doc/1"
```

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/2.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/3.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/4.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/5.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/6.png )

```
curl -X DELETE -H accept:application/json -H Content-type:application/json "localhost:9200/test_index/_doc/1"
```

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/7.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/8.png )

```
curl -X GET -H accept:application/json -H Content-type:application/json "localhost:9200/test_index/_search"
```

	- Will return ALL documents, we DO NOT specify any parameters.

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/9.png )

```
curl -X GET -H accept:application/json -H Content-type:application/json "http://localhost:9200/test_index/_doc/2"
```

	- find by a specific id
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/terminal/10.png )	

[(7:00)]( https://youtu.be/Dg5pztsa80c?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=420 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/3lcs/18.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/3lcs/19.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/3lcs/20.png )

* ***POSTMAN:***

```
PUT
http://localhost:9200/test_index/_doc/1
{ "title": "Fighting Ebola with Elastic", "category": "User Stories", "author": { "first_name": "Emily", "last_name": "Mother"} }
```

Error:

_- "error":"Content-Type header [text/plain] is not supported","status":406}_

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/postman/1.png )

<https://stackoverflow.com/questions/30511911/getting-not-supported-media-type-error>

- SET `Headers` under `Request`:

	KEY 			VALUE	
	
	Content-type 	application/json
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/postman/2.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/1elastic_sandbox_and_lcs/postman/3.png )
	
---

[4 ElasticSearch параметры поиска search - уроки ElasticSearch (9:45)]( https://www.youtube.com/watch?v=T3-t0180VC4&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&index=4&ab_channel=LiveCodingSchool )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/7.png )

```
GET blogs/_search

{
	"query": {
		"match": {
			"content": {
				"query": "ingest nodes",
				"operator": "and"
			}
		}
	}
}

GET blogs/_search?q=content:( ingest AND nodes )
```

[(1:45)]( https://youtu.be/T3-t0180VC4?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=105 )

```
{
	"query": {
		"match": {
			"content": {
				"query": "ingest nodes logstash",
				"minimum_should_match": 2
			}
		}
	}
}
```

[(2:25)]( https://youtu.be/T3-t0180VC4?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=145 )

```
{
	"query": {
		"match_phrase": {
			"content": {
				"query": "open data",
				"slop": 1
			}
		}
	}
}
```

	- "slop" - "jump over", IF it is necessary to indicate that there can be a word between.

```
{
	"query": {
		"range": {
			"publish_date": {
				"gte": "2017:12:01",
				"lt": "2018:01:01"
			}
		}
	}
}
```

[(4:50)]( https://youtu.be/T3-t0180VC4?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=290 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/7.png )

```
{
	"query": {
		"bool": {
			"must": {
				"match": {
					"content": "logstash"
				}
			},
			"must_not": {
				"match": {
					"category": "releases"
				}
			}
		}
	}
}
```

[(7:05)]( https://youtu.be/T3-t0180VC4?list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&t=425 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/8.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/9.png )

```
{
	"query": {
		"bool": {
			"must": {
				"match_phrase": {
					"content": "elastic stack"
				}
			},
			"should": {
				"match_phrase": {
					"author": "shay banon"
				}
			}
		}
	}
}
```

	- "should" - Higher priority with author "shay banon"- higher "score".

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/10.png )

```
{
	"query": {
		"bool": {
			"must": {
				"match_phrase": {
					"content": "elastic stack"
				}
			},
			"filter": {
				"range": {
					"publish_date": {						
						"lt": "2017:01:01"
					}
				}
			}
		}
	}
}
```

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/11.png )

`"must"` + `"should"` - More relevant search:

```
{
	"query": {
		"bool": {
			"must": [
				{"match": {"title": "elastic"}}
			],
			"should": [
				{"match": {"title": "stack"}}
				{"match": {"title": "query"}}
				{"match": {"title": "speed"}}
			]
		}
	}
}
```

	- with title "stack", "query", "speed" - will be higher than the others.

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4lcs/12.png )

#### useful links:

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html>

<https://hub.docker.com/_/elasticsearch/?ref=login>

[Live Coding School - ElasticSearch]( https://www.youtube.com/watch?v=qDt70R4i3wk&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&ab_channel=LiveCodingSchool )

INSTALL POSTMAN for Firefox.

<https://linuxthebest.net/kak-ustanovit-portman-v-ubuntu-16-04-18-04/>

Possible Errors:

<https://stackoverflow.com/questions/51378099/content-type-header-not-supported> 

<https://stackoverflow.com/questions/30511911/getting-not-supported-media-type-error>