# Elastic Python Workshop #2 

## useful classes for admins 

You can find here the code in full length for the workshop [Elastic Python Workshop #2 – useful classes for admins]()

```
from ssl import create_default_context
from elasticsearch import Elasticsearch
import json

api_key='aC1wNUYzOEJCWV9zaUd4ZW1PMkg6REFfQ29JcDFRSjJMaEhvbDMyWElvZw=='
context = create_default_context(cafile='/home/pascal/python_es_client.pem')
es = Elasticsearch(["https://srvelk8:9200"], ssl_context=context, api_key=api_key)
es.cat.nodes()
```
## pretty print

```
info = es.xpack.info()
print(json.dumps(info, indent=4, sort_keys=True))
```
even shorter


```
print(json.dumps(es.cluster.health(), indent=4, sort_keys=True))
print(json.dumps(es.cluster.state(), indent=4, sort_keys=True))
```

