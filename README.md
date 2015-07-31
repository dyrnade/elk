# ELK STACK FOR COREOS(JOURNALD) #

### Download ElasticSearch Docker ###
- https://registry.hub.docker.com/u/library/elasticsearch/

```bash
 docker pull elasticsearch
```
### Download Logstash Docker ###
- https://registry.hub.docker.com/_/logstash/

```bash
 docker pull logstash
```
### Download Kibana Docker ###
- https://registry.hub.docker.com/u/library/kibana/

```bash
docker pull kibana
```

### Run ElasticSearch container ###

- ElasticSearch runs at port 9200

```bash
sudo docker run -d -p 9200:9200 -p 9300:9300 --name elasticsearch_container elasticsearch
```

### Run Kibana container ###

- Kibana runs at port 5601

```bash
sudo docker run -d --name kibana_container -e ELASTICSEARCH_URL=http://$COREOS_PRIVATE_IPV4:9200 -p 5601:5601 kibana
```

### Run Logstash container ###

- Download logstash.conf and create config-dir directory and put logstash.conf in it.

```bash
cd config-dir
sudo docker run -it -d -p 5000:5000/udp --name logstash_container -v "$PWD":/config logstash logstash -f /config/logstash.conf
```

### Send journald logs to logstash container ###

```bash

journalctl -o short -f | ncat --udp localhost 5000
```


### After running logstash container type some inputs and to see results ###

For ElasticSearch

```bash
curl http://localhost:9200/_search?pretty
```

For Kibana

```bash
http://localhost:5601
```
