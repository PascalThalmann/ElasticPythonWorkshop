# Elastic Python Workshop #1 – the basics

You can find here the code in full length for the workshop [Elastic Python Workshop #1 – the basics](https://cdax.ch/2022/02/20/elasticsearch-python-workshop-1-the-basics/)

## Install the library

```
sudo apt update && sudo apt upgrade
sudo apt install python3-pip
sudo python3 -m pip install 'elasticsearch>=7.0.0,<8.0.0'
sudo python3 -m pip install elasticsearch_dsl
```

## Create your first connection

```
es = Elasticsearch(["http://srvelk:9200"])
es.cat.nodes()
```

## Create a connection with security enabled

### install urllib3

```
sudo python3 -m pip install urllib3
```

### create the connection

```
from ssl import create_default_context
from elasticsearch import Elasticsearch

es = Elasticsearch(["https://username:password@srvelk:9200"], verify_certs=False)
es.cat.nodes()
```

## Generate the pem certificate

### read and generate the certificate

```
/usr/share/elasticsearch/bin/elasticsearch-keystore \
   show xpack.security.http.ssl.keystore.secure_password

openssl pkcs12 -in /etc/elasticsearch/certs/http.p12 \
   -cacerts -out /etc/elasticsearch/certs/python_es_client.pem

chmod 666 /etc/elasticsearch/certs/python_es_client.pem
cp /etc/elasticsearch/certs/python_es_client.pem /tmp
```

### use the certificate

```
from ssl import create_default_context
from elasticsearch import Elasticsearch

context = create_default_context(cafile='/tmp/python_es_client.pem')
es = Elasticsearch(["https://username:password@srvelk:9200"], ssl_context=context)
es.cat.nodes()
```

## Connect with API key


```
from ssl import create_default_context
from elasticsearch import Elasticsearch

api_key='aC1wNUYzOEJCWV...RSjJMaEhvbDMyWElvZw=='
context = create_default_context(cafile='/tmp/python_es_client.pem')
es = Elasticsearch(["https://srvelk:9200"], ssl_context=context, api_key=api_key)
es.cat.nodes()
```


