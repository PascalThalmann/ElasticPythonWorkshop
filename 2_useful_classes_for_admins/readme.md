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


```
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
