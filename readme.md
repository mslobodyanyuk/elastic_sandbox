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