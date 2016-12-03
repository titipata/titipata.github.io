---
title: elastic search in python
---

Elastic Search is one of the great backbone for searching application.
In this post, we are going to explore how to index database with [*elasticsearch*](https://www.elastic.co/)
(or its new name *elastic*
using [elasticsearch-py](https://github.com/elastic/elasticsearch-py).
I'm not writing this blog post myself but it's based on this [post](https://qbox.io/blog/building-an-elasticsearch-index-with-python)

First, we have to install elastic from [download page](https://www.elastic.co/downloads/elasticsearch).
Or if you have [Homebrew](http://brew.sh/), you can install it using `brew install elasticsearch`.

Then run `elasticsearch`, i.e. `./bin/elasticsearch` if you download the folder or
`elasticsearch` for Homebrew.

Here is an example on how to add index for example titanic dataset in Python.

```python
import pandas as pd
from urllib.request import urlopen
from elasticsearch import Elasticsearch

url = "http://apps.sloanahrens.com/qbox-blog-resources/kaggle-titanic-data/test.csv"
index_name = 'titanic'
type_name = 'passenger'
id_field = 'passengerid'

titanic_df = pd.read_csv(urlopen(url)).fillna('')
titanic_records = df.to_dict(orient='records')

es = Elasticsearch()
if not es.indices.exists(index_name):
    es.indices.create(index_name, ignore=400)

actions = []
for i, r in enumerate(titanic_records):
    actions.append({"_index": index_name,
                    "_type": type_name,
                    "_id": i,
                    "_source": r})

helpers.bulk(es, actions=actions)
```

Other useful snippets include

```python
es.indices.get_aliases().keys() # get list of all index
```

```python
es.search(index='titanic', q="C.A.", size=20)['hits']['hits'] # search C.A. from `titanic` index for 20 results
```

```python
es.count(index_name) # count how many we've indexed in `titanic`
```

```python
es.indices.delete(index=index_name, ignore=[400, 404]) # delete index
```
