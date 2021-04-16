"SANDBOX" for Testing Elasticsearch( - show how curl requests are processed )
=============================================================================

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html>

<https://hub.docker.com/_/elasticsearch/?ref=login>

Now(`9.04.2021`), current versions of `Elasticsearch`( `7.12.0` OR `6.8.15` ).

---

Live Coding School

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

	KEY             VALUE	
	Content-type    application/json
	
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

	- `"slop"` - "jump over", IF it is necessary to indicate that there can be a word between.

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

	- `"should"` - Higher priority with author `"shay banon"`- higher `score`.

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

Live Coding School

[Live Coding School - ElasticSearch]( https://www.youtube.com/watch?v=qDt70R4i3wk&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&ab_channel=LiveCodingSchool )

INSTALL POSTMAN for Firefox.

<https://linuxthebest.net/kak-ustanovit-portman-v-ubuntu-16-04-18-04/>

Possible Errors:

<https://stackoverflow.com/questions/51378099/content-type-header-not-supported> 

<https://stackoverflow.com/questions/30511911/getting-not-supported-media-type-error>

---

Dima Neman

[Dima Neman - ElasticSearch( 1-6 videos ~2h:20 min. )]( https://www.youtube.com/watch?v=bHNyiVKyZMI&list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&ab_channel=DimaNeman )

[Dima Neman - ElasticSearch - 01. Основные понятия. CRUD-операции. (41:45)]( https://www.youtube.com/watch?v=bHNyiVKyZMI&list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&ab_channel=DimaNeman )

_The author of the video has ElasticSearch version `7.6`. - I have version `6.8.15`, one of the most up-to-date on (`12.04.2021`)._

	docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.8.15

Error:

_docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?. See 'docker run --help'._

<https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker>
	
	sudo systemctl start docker

_If you are using curl, then add the "?pretty=true" or "?pretty" parameter to the request, the output becomes more readable._

	curl -X GET "localhost:9200"
	curl -X GET "localhost:9200/_cat/nodes?v=true&pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/1.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/2.png )

[(4:45)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=285 ) There are two types of `Mapping`, `static` and `dynamic`. `Mapping` is NOT ONLY a schema. Through `Mapping` you can set how to search for documents.

[(12:15)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=735 )

	curl -X GET "localhost:9200/_cat/indices"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/3.png )

* ***CRUD operations.:***

[(13:00)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=780 ) Create index:

	curl -XPUT "localhost:9200/prods?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/4.png )

[(13:30)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=810 ) Delete index:

	curl -XDELETE "localhost:9200/prods?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/5.png )

[(16:20)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=980 ) Let's create in a more correct way, pass `Mappings`:

<https://www.elastic.co/guide/en/elasticsearch/reference/6.8/mapping.html>	

```
curl -XPUT 'localhost:9200/persons?pretty' -H 'Content-Type: application/json' -d '{
"mappings" : {
"_doc" : {
"properties" : {
"name" : {"type" : "text"}, "age" : {"type" : "integer"} } } } }'
```

	curl -XPUT 'localhost:9200/persons?pretty' -H 'Content-Type: application/json' -d '{ "mappings" : { "_doc" : { "properties" : {	"name" : {"type" : "text"}, "age" : {"type" : "integer"} } } } }'
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/6.png )

[(18:45)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1125 ) Es "complains" that you have very little space left on the "screw", And it inserts `"read_only_allow_delete"` by default:

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/7.png )

[(19:05)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1145 ) Now - "false":

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/8.png )

	- "De facto", it will have to be done every time.

[(21:20)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1280 )	

	curl -XPOST 'localhost:9200/persons/_doc' -H 'Content-Type: application/json' -d '{ "name" : "dima", "age" : 11 }'

[(21:25)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1285 ) Just about this mistake he said, "that I have little space and he complains":

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/9.png )

As we can see, the `id` was automatically assigned:

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/10.png )

[(23:35)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1415 ) Get (- apply), by document `id`:

	curl -X GET "localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/11.png )

	- In earlier versions, after "_doc" would indicate the document type.
	
[(26:30)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1590 ) Let's insert a new object, add a new field:

	curl -XPOST 'localhost:9200/persons/_doc' -H 'Content-Type: application/json' -d '{ "name" : "eugene", "age" : 12, "sex" : "m" }'

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/12.png )

	curl -X GET "localhost:9200/persons/_doc/HNLRxXgBWvajBkcHbAuq?pretty"
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/13.png )	

[(28:20)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1700 )

	curl -X GET "localhost:9200/persons?pretty"
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/14.png )

[(29:05)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1745 ) Create document with `id`:

	curl -XPOST 'localhost:9200/persons/_doc/3' -H 'Content-Type: application/json' -d '{ "name" : "eugene", "age" : 12, "sex" : "m" }'
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/15.png )	

	curl -X GET "localhost:9200/persons/_doc/3?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/16.png )

[(30:20)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=1820 )

	curl -XDELETE "localhost:9200/persons/_doc/3?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/17.png )
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/18.png )

[(33:50)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=2030 ) In `Content-Type`, through the `json-object`, we will constantly define what we want to do with `ElasticSearch`. - In fact, I described what I want to find.
	
	curl -XGET "localhost:9200/persons/_search?pretty"  -H 'Content-Type: application/json' -d '{ "query" : {"bool" : { "filter" : [ {"term" : { "name" : "dima" }}] }} }'

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/19.png )

[(37:25)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=2245 ) Update document, `_update`:

	curl -X GET "localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth?pretty"

<https://www.elastic.co/guide/en/elasticsearch/reference/6.8/docs-update.html>
			
	curl -XPOST 'localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth/_update?pretty' -H 'Content-Type: application/json' -d '{ "doc" : { "name" : "dimaneman" } }'

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/20.png )

[(37:50)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=2270 ) Find by `_search`:

	curl -XGET "localhost:9200/persons/_search?pretty"  -H 'Content-Type: application/json' -d '{ "query" : {"bool" : { "filter" : [ {"term" : { "name" : "dimaneman" }}] }} }'

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/21.png )

[(38:05)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=2285 ) More beautiful:
	
	curl -X GET "localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/22.png )

[(38:25)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=2305 ) Change the field value for `_update`. As you can see, the `field` and `version` have changed:

	curl -XPOST 'localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth/_update?pretty' -H 'Content-Type: application/json' -d '{ "doc" : { "name" : "dimaneman2" } }'

	curl -X GET "localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/23.png )	

[(39:50)]( https://youtu.be/bHNyiVKyZMI?list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&t=2390 ) In addition to classic queries, you can also write code. - How do you change, under what conditions do you change.
Add age:

	curl -XPOST 'localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth/_update?pretty' -H 'Content-Type: application/json' -d '{ "script" : { "source" : "ctx._source.age++" } }'
	
	curl -X GET "localhost:9200/persons/_doc/G9K6xXgBWvajBkcH7wth?pretty"

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/2elastic_sandbox_dneman/24.png )

	- As we remember, it was "11", became - "12".

ElasticSearch allows you to make so-called "script requests" in a special language called `painless`. - Through it, you can describe how you can "knock" on the object, how you can change it, change it.

<https://www.elastic.co/guide/en/elasticsearch/reference/master/modules-scripting-painless.html>

#### useful links:

Dima Neman

[Dima Neman - ElasticSearch]( https://www.youtube.com/watch?v=bHNyiVKyZMI&list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&ab_channel=DimaNeman )

ElasticSearch

<https://www.elastic.co/guide/en/elasticsearch/reference/6.8/mapping.html>	

<https://www.elastic.co/guide/en/elasticsearch/reference/6.8/docs-update.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/master/modules-scripting-painless.html>

Possible Errors:

<https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker>

---

Kemal Yenilmez

[Kemal Yenilmez - Docker Elasticsearch PHP CRUD (4:33)]( https://www.youtube.com/watch?v=2nWSPMmLdeE&ab_channel=KemalYenilmez )

Sources at github:
	
<https://github.com/kemalyen/elasticsearch-php-docker>

* ***- Development docker. It contains PHP 7, MariaDb, Elastic search, nginx***
	
[(0:45)]( https://youtu.be/2nWSPMmLdeE?t=45 )
	
	docker-compose up -d	
	
[(1:15)]( https://youtu.be/2nWSPMmLdeE?t=75 )

	composer require elasticsearch/elasticsearch	
	
[(2:15)]( https://youtu.be/2nWSPMmLdeE?t=135 ) Indexing a document.

[(2:35)]( https://youtu.be/2nWSPMmLdeE?t=155 ) Searching.

[(3:30)]( https://youtu.be/2nWSPMmLdeE?t=210 ) Updating a document.

[(4:10)]( https://youtu.be/2nWSPMmLdeE?t=250 ) Getting a document.

#### useful links:

Kemal Yenilmez 

[Docker Elasticsearch PHP CRUD]( https://www.youtube.com/watch?v=2nWSPMmLdeE&ab_channel=KemalYenilmez )

<https://github.com/kemalyen/elasticsearch-php-docker>

---

Izweb Technologies

[Izweb Technologies - Docker Images - ElasticSearch (6:36)]( https://www.youtube.com/watch?v=4SGUox3ZTe0&ab_channel=IzwebTechnologies ) 

In this video you are going to learn about ElasticSearch on Docker.

a powerful open source search and analytics engine that makes data easy to explore.
an open source distributed, RESTful search and analytics engine capable of solving a growing number of use cases.
a database that stores, retrieves, and manages document-oriented and semi-structured data
When you use Elasticsearch, you store data in JSON document form. Then, you query them for retrieval...

<https://www.elastic.co/>

[(2:20)]( https://youtu.be/4SGUox3ZTe0?t=140 )

<https://labs.play-with-docker.com/>

[(3:00)]( https://youtu.be/4SGUox3ZTe0?t=180 )

	docker run -d -p 9200:9200 -e "discovery.type=single-node" \ -v esdata:/usr/share/elasticsearch/data \ docker.elastic.co/elasticsearch/elasticsearch:6.8.15

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/1.png )

[(3:45)]( https://youtu.be/4SGUox3ZTe0?t=225 )

	docker ps

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/2.png )

[(3:55)]( https://youtu.be/4SGUox3ZTe0?t=235 ) Usage - Check cluster health.

	curl http://localhost:9200/_cluster/health?pretty

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/3.png )	

[(4:30)]( https://youtu.be/4SGUox3ZTe0?t=270 ) Usage - Create an index.

	curl -X PUT "localhost:9200/customer?pretty"
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/4.png )	
		
[(4:45)]( https://youtu.be/4SGUox3ZTe0?t=285 ) And let's add a document to this index.

	curl -X PUT "localhost:9200/customer/_doc/1?pretty" \ -H 'Content-Type: application/json' -d '{ "name" : "Mark Heath" }'

Error:	
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/5.png )

<https://discuss.elastic.co/t/regarding-to-add-a-header-h-content-type-application-json/198363>

	curl -XPUT "localhost:9200/customer/_doc/1?pretty" -H 'Content-Type: application/json' -d ' { "name" : "Mark Heath" , "settings" : { "index.mapping.total_fields.limit" : "2000" } }'
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/6.png )		

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/7.png )

[(5:00)]( https://youtu.be/4SGUox3ZTe0?t=300 ) Usage - View documents in the index.

	curl localhost:9200/customer/_search?pretty

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/8.png )

[(5:35)]( https://youtu.be/4SGUox3ZTe0?t=335 ) Usage - Check our index is still present.

	curl -XPUT "localhost:9200/customer/_doc/2?pretty" -H 'Content-Type: application/json' -d ' { "name" : "Steph Heath" }'
	
![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/9.png )

[(6:05)]( https://youtu.be/4SGUox3ZTe0?t=365 )	

	curl localhost:9200/customer/_search?pretty	

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/4elastic_sandbox_izweb/10.png )

#### useful links:	

Izweb Technologies

[Docker Images - ElasticSearch]( https://www.youtube.com/watch?v=4SGUox3ZTe0&ab_channel=IzwebTechnologies )

<https://www.elastic.co/>

<https://labs.play-with-docker.com/>

Possible Errors:

<https://discuss.elastic.co/t/regarding-to-add-a-header-h-content-type-application-json/198363>

---

Just me and Opensource

[Just me and Opensource - [ Elasticsearch 6 ] Running Elasticsearch v7.1.1 in Docker containers (13:05)]( https://www.youtube.com/watch?v=PWUuyDrqvt0&ab_channel=JustmeandOpensource )

In this video, I will show you how to run elasticsearch and Kibana version 7.1.1 in Docker containers.

Github:

<https://github.com/justmeandopensource/elk>

Elasticsearch Official site:

<https://www.elastic.co/>

[(1:45)]( https://youtu.be/PWUuyDrqvt0?t=105 )

	git clone https://github.com/justmeandopensource/elk
	
[(2:25)]( https://youtu.be/PWUuyDrqvt0?t=145 ) Single container `elastic 6.5.4` and `Kibana` single container:	

	docker-compose.yml

[(3:45)]( https://youtu.be/PWUuyDrqvt0?t=225 ) Single container `elastic 7.1.1` and `Kibana` single container. There's additional options for 7.1.1 version.

[(5:30)]( https://youtu.be/PWUuyDrqvt0?t=330 )

	docker-compose up -d
	
[(7:10)]( https://youtu.be/PWUuyDrqvt0?t=430 ) See the docker-compose logs files to see the `elastic` and `Kibana` is getting started:

	cd elk/docker
	
	docker-compose logs -f

	docker-compose logs -f elasticsearch
	
[(7:40)]( https://youtu.be/PWUuyDrqvt0?t=460 ) - Elasticsearch excited with code 78. 

The vital step you must do is to set the kernel parameter:

	sysctl -w vm.max_map_count=262144

[(8:25)]( https://youtu.be/PWUuyDrqvt0?t=505 ) To take effect immediately:
	
	sudo sysctl -w vm.max_map_count=262144
	
 - IF you want to make this change permanent you have to write it to the `/etc/sysctl.conf` OR `/etc/sysctl.d/any_name_you_can_give`.
	
[(9:05)]( https://youtu.be/PWUuyDrqvt0?t=545 )

	docker-compose restart elasticsearch
	
[(9:20)]( https://youtu.be/PWUuyDrqvt0?t=560 )
	
	docker-compose logs -f elasticsearch

Cluster health status change from `yellow` to `green`. - It should be working.

	docker-compose ps
	sudo netstat -nltp

[(10:00)]( https://youtu.be/PWUuyDrqvt0?t=600 ) `In Browser`:
	
	localhost:5601
	
	- Kibana dashboard loading.
	
#### useful links:	

Just me and Opensource

[[ Elasticsearch 6 ] Running Elasticsearch v7.1.1 in Docker containers]( https://www.youtube.com/watch?v=PWUuyDrqvt0&ab_channel=JustmeandOpensource )

<https://github.com/justmeandopensource/elk>

Elasticsearch Official site:

<https://www.elastic.co/>

Possible Errors:

[(7:40) - Elasticsearch excited with code 78.]( https://youtu.be/PWUuyDrqvt0?t=460 )

---

Codetuber

[Codetuber - Painless scripting in Elasticsearch | [Elasticsearch 7 for beginners #5.4] (15:53)]( https://www.youtube.com/watch?v=a3OgrYj3ja0&ab_channel=Codetuber )

In this elasticsearch 7 tutorial, we discuss about scripting in elasticsearch. 

Timings

[0:00​]( https://youtu.be/a3OgrYj3ja0?t=0 ) - What is scripting?

[0:45​]( https://youtu.be/a3OgrYj3ja0?t=45 )​ - Painless scripting language

[1:51​]( https://youtu.be/a3OgrYj3ja0?t=111 )​​ - Lucene expressions Language

[2:20​]( https://youtu.be/a3OgrYj3ja0?t=140 )​​ - How to use scripting in elasticsearch?

[4:00​]( https://youtu.be/a3OgrYj3ja0?t=240 )​​ - Performing string concatenation using elasticsearch scripting

[6:30​]( https://youtu.be/a3OgrYj3ja0?t=390 )​​ - Performing arithmetic using elasticsearch scripting

[7:45​]( https://youtu.be/a3OgrYj3ja0?t=465 )​​ - Using parameters in elasticsearch scripting

[10:20​]( https://youtu.be/a3OgrYj3ja0?t=620 )​​ - Saving scripts in elasticserach

[11:30​]( https://youtu.be/a3OgrYj3ja0?t=690 )​​ - Using saved scripts in elasticsearch 

[12:25​]( https://youtu.be/a3OgrYj3ja0?t=745 )​​ - Bulk update using _update_by_query and elasticsearch scripting

[14:30​]( https://youtu.be/a3OgrYj3ja0?t=870 )​​ - Context variable used for updates

[15:50​]( https://youtu.be/a3OgrYj3ja0?t=950 )​​ - Using elasticsearch scripting with aggregations

Entire Playlist: 

[Elasticsearch 7 for Beginners]( https://www.youtube.com/watch?v=lnEzmQHa6Co&list=PLa6iDxjj_9qVaf5CsXWP-GAgZoVwKowjx&ab_channel=Codetuber )

Links:

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-painless.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-expression.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-using.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update-by-query.html>

With scripting, you can evaluate custom expressions in Elasticsearch. For example, you could use a script to return "script fields" as part of a search request or evaluate a custom score for a query.
The default scripting language is Painless. Additional lang plugins enable you to run scripts written in other languages. Everywhere a script can be used, you can include a lang parameter to specify the language of the script.

General-purpose languagesedit

These languages can be used for any purpose in the scripting APIs, and give the most flexibility.

Languages

	painless
	expression
	mustache
	java

Scripts and security

Languages that are sandboxed are designed with security in mind. However, non- sandboxed languages can be a security issue, please read Scripting and security for more details.
Updates documents that match the specified query. If no query is specified, performs an update on every document in the data stream or index without modifying the source, which is useful for picking up mapping changes.

[0:00​]( https://youtu.be/a3OgrYj3ja0?t=0 ) - What is scripting?

[0:45​]( https://youtu.be/a3OgrYj3ja0?t=45 )​ - Painless scripting language

[1:51​]( https://youtu.be/a3OgrYj3ja0?t=111 )​​ - Lucene expressions Language

[2:20​]( https://youtu.be/a3OgrYj3ja0?t=140 )​​ - How to use scripting in elasticsearch?

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/1.png )

[3:40]( https://youtu.be/a3OgrYj3ja0?t=220 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/2.png )

[4:00​]( https://youtu.be/a3OgrYj3ja0?t=240 )​​ - Performing string concatenation using elasticsearch scripting

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/3.png )

[5:25]( https://youtu.be/a3OgrYj3ja0?t=325 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/4.png )

[6:20]( https://youtu.be/a3OgrYj3ja0?t=380 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/5.png )

[6:30​]( https://youtu.be/a3OgrYj3ja0?t=390 )​​ - Performing arithmetic using elasticsearch scripting

[7:15]( https://youtu.be/a3OgrYj3ja0?t=435 )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/6.png )

[7:45​]( https://youtu.be/a3OgrYj3ja0?t=465 )​​ - Using parameters in elasticsearch scripting

[7:55​]( https://youtu.be/a3OgrYj3ja0?t=475 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/7.png )

[8:50​]( https://youtu.be/a3OgrYj3ja0?t=530 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/8.png )

[9:25​]( https://youtu.be/a3OgrYj3ja0?t=565 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/9.png )

[10:20​]( https://youtu.be/a3OgrYj3ja0?t=620 )​​ - Saving scripts in elasticserach

[10:35​]( https://youtu.be/a3OgrYj3ja0?t=635 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/10.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/11.png )

[11:15​]( https://youtu.be/a3OgrYj3ja0?t=675 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/12.png )

[11:30​]( https://youtu.be/a3OgrYj3ja0?t=690 )​​ - Using saved scripts in elasticsearch 

[12:05​]( https://youtu.be/a3OgrYj3ja0?t=725 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/13.png )

[12:25​]( https://youtu.be/a3OgrYj3ja0?t=745 )​​ - Bulk update using _update_by_query and elasticsearch scripting

[13:55​]( https://youtu.be/a3OgrYj3ja0?t=835 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/14.png )

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/15.png )

[14:30​]( https://youtu.be/a3OgrYj3ja0?t=870 )​​ - Context variable used for updates

[15:05​]( https://youtu.be/a3OgrYj3ja0?t=905 ) 

![screenshot of sample]( https://github.com/mslobodyanyuk/elastic_sandbox/blob/master/public/images/6elastic_sandbox_codetuber/16.png )

[15:50​]( https://youtu.be/a3OgrYj3ja0?t=950 )​​ - Using elasticsearch scripting with aggregations

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting.html>

#### useful links:

Codetuber

[Painless scripting in Elasticsearch | [Elasticsearch 7 for beginners #5.4]]( https://www.youtube.com/watch?v=a3OgrYj3ja0&ab_channel=Codetuber )

Entire Playlist: 

[Elasticsearch 7 for Beginners]( https://www.youtube.com/watch?v=lnEzmQHa6Co&list=PLa6iDxjj_9qVaf5CsXWP-GAgZoVwKowjx&ab_channel=Codetuber )

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-painless.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-expression.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-using.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update-by-query.html>

#### Useful links:

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html>

<https://hub.docker.com/_/elasticsearch/?ref=login>

Live Coding School

[Live Coding School - ElasticSearch]( https://www.youtube.com/watch?v=qDt70R4i3wk&list=PLdpb__6uY73kCu4eG9IolmhkBmNgyRL-i&ab_channel=LiveCodingSchool )

INSTALL POSTMAN for Firefox.

<https://linuxthebest.net/kak-ustanovit-portman-v-ubuntu-16-04-18-04/>

Possible Errors:

<https://stackoverflow.com/questions/51378099/content-type-header-not-supported> 

<https://stackoverflow.com/questions/30511911/getting-not-supported-media-type-error>

Dima Neman

[Dima Neman - ElasticSearch]( https://www.youtube.com/watch?v=bHNyiVKyZMI&list=PLtHDJri4AWWSVminwcA3cS9CdSlvkvQ-J&ab_channel=DimaNeman )

ElasticSearch

<https://www.elastic.co/guide/en/elasticsearch/reference/6.8/mapping.html>	

<https://www.elastic.co/guide/en/elasticsearch/reference/6.8/docs-update.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/master/modules-scripting-painless.html>

Possible Errors:

<https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker>

Kemal Yenilmez 

[Docker Elasticsearch PHP CRUD]( https://www.youtube.com/watch?v=2nWSPMmLdeE&ab_channel=KemalYenilmez )

<https://github.com/kemalyen/elasticsearch-php-docker>

Izweb Technologies

[Docker Images - ElasticSearch]( https://www.youtube.com/watch?v=4SGUox3ZTe0&ab_channel=IzwebTechnologies )

<https://www.elastic.co/>

<https://labs.play-with-docker.com/>

Possible Errors:

<https://discuss.elastic.co/t/regarding-to-add-a-header-h-content-type-application-json/198363>

Just me and Opensource

[[ Elasticsearch 6 ] Running Elasticsearch v7.1.1 in Docker containers]( https://www.youtube.com/watch?v=PWUuyDrqvt0&ab_channel=JustmeandOpensource )

<https://github.com/justmeandopensource/elk>

Elasticsearch Official site:

<https://www.elastic.co/>

Possible Errors:

[(7:40) - Elasticsearch excited with code 78.]( https://youtu.be/PWUuyDrqvt0?t=460 )

Codetuber

[Painless scripting in Elasticsearch | [Elasticsearch 7 for beginners #5.4]]( https://www.youtube.com/watch?v=a3OgrYj3ja0&ab_channel=Codetuber )

Entire Playlist: 

[Elasticsearch 7 for Beginners]( https://www.youtube.com/watch?v=lnEzmQHa6Co&list=PLa6iDxjj_9qVaf5CsXWP-GAgZoVwKowjx&ab_channel=Codetuber )

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-painless.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-expression.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-scripting-using.html>

<https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update-by-query.html>