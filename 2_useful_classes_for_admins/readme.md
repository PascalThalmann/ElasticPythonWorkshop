# Elastic Python Workshop #2 

## objects, classes, and how to call them

You can find here the code in full length for the workshop [Elastic Python Workshop #2 – useful classes for admins](https://cdax.ch/2022/02/24/elasticsearch-python-workshop-2-objects-classes-and-how-to-call-them/)

```
from elasticsearch import Elasticsearch
es = Elasticsearch(["https://username:password@srvelk:9200"], verify_certs=False)
```
## Elasticsearch class

### Create an index and a document

```
status = es.create(index='testidx', id=1, document='{"item": "content"}')
print(json.dumps(status, indent=4))
```

> {
    "_index": "testidx",
    "_id": "1",
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 0,
    "_primary_term": 1
 }

```
if status['result'] == 'created':
   print("document created")
```

### Get a document


```
status = es.get(index='textidx', id=1)
print(json.dumps(status, indent=4))
```
> {
    "_index": "textidx",
    "_id": "1",
    "_version": 1,
    "_seq_no": 0,
    "_primary_term": 1,
    "found": true,
    "_source": {
        "item": "content"
    }
 }

### Search documents


```
es.search(index="testidx", body={
  "query": {
     "match_all": {}
   }
 })
```

## Using the CatClient Class (and any other)


```
>>> elasticsearch.client.cat.CatClient(es).nodes()
'192.168.1.68 44 85 1 0.07 0.04 0.01 cdfhilmrstw * srvelk8\n'
```

```
print(es.__dict__['cat'])

for key, value in es.__dict__.items():
   vl = str(value).split(" ")[0].strip()
   print("{0:<20s} {1:>70s}".format(key.strip(), vl))

transport                                                <elasticsearch.transport.Transport
async_search                           <elasticsearch.client.async_search.AsyncSearchClient
autoscaling                             <elasticsearch.client.autoscaling.AutoscalingClient
cat                                                     <elasticsearch.client.cat.CatClient
ccr                                                     <elasticsearch.client.ccr.CcrClient
cluster                                         <elasticsearch.client.cluster.ClusterClient
dangling_indices               <elasticsearch.client.dangling_indices.DanglingIndicesClient
data_frame                                <elasticsearch.client.data_frame.Data_FrameClient
deprecation                             <elasticsearch.client.deprecation.DeprecationClient
enrich                                            <elasticsearch.client.enrich.EnrichClient
eql                                                     <elasticsearch.client.eql.EqlClient
features                                      <elasticsearch.client.features.FeaturesClient
fleet                                               <elasticsearch.client.fleet.FleetClient
graph                                               <elasticsearch.client.graph.GraphClient
ilm                                                     <elasticsearch.client.ilm.IlmClient
indices                                         <elasticsearch.client.indices.IndicesClient
ingest                                            <elasticsearch.client.ingest.IngestClient
license                                         <elasticsearch.client.license.LicenseClient
logstash                                      <elasticsearch.client.logstash.LogstashClient
migration                                   <elasticsearch.client.migration.MigrationClient
ml                                                        <elasticsearch.client.ml.MlClient
monitoring                                <elasticsearch.client.monitoring.MonitoringClient
nodes                                               <elasticsearch.client.nodes.NodesClient
remote                                            <elasticsearch.client.remote.RemoteClient
rollup                                            <elasticsearch.client.rollup.RollupClient
searchable_snapshots   <elasticsearch.client.searchable_snapshots.SearchableSnapshotsClient
security                                      <elasticsearch.client.security.SecurityClient
shutdown                                      <elasticsearch.client.shutdown.ShutdownClient
slm                                                     <elasticsearch.client.slm.SlmClient
snapshot                                      <elasticsearch.client.snapshot.SnapshotClient
sql                                                     <elasticsearch.client.sql.SqlClient
ssl                                                     <elasticsearch.client.ssl.SslClient
tasks                                               <elasticsearch.client.tasks.TasksClient
text_structure                     <elasticsearch.client.text_structure.TextStructureClient
transform                                   <elasticsearch.client.transform.TransformClient
watcher                                         <elasticsearch.client.watcher.WatcherClient
xpack                                               <elasticsearch.client.xpack.XPackClient
```
## Some usefull stuff

```
es.info()
es.cat.indices()
es.xpack.info()
es.cluster.health()
```
