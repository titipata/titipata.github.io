---
title: pyspark 2.1 few tips
---

this is a small snippet on notebook to print out executors link. sometimes,
we want to check executor link.

```python
from IPython.display import HTML, display
url = spark.conf.get('spark.org.apache.hadoop.yarn.server.webproxy.amfilter.AmIpFilter.param.PROXY_URI_BASES') + '/executors/'
HTML("<a href=\"{0}\" target='_blank'>{0}</a>".format(url))
```
