### Download ElasticSearch Docker ###

```bash
 docker pull elasticsearch
```
### Download Logstash Docker ###

```bash
 docker pull logstash
```
### Download Kibana Docker ###

```bash
docker pull kibana
```

### Run ElasticSearch container ###

- ElasticSearch runs at port 9200

```bash
sudo docker run --rm --name my-elasticsearch elasticsearch
```

### Run Logstash container ###

- Download logstash.conf and create config-dir directory and put logstash.conf in it.

```bash
cd config-dir
sudo docker run -it --rm -v "$PWD":/config-dir logstash logstash -f /config-dir/log.conf
```

### Run Kibana container ###

- Kibana runs at port 5601

```bash
sudo docker run --rm --name my-kibana -e ELASTICSEARCH_URL=http://$COREOS_PRIVATE_IPV4:9200 -P kibana
```
