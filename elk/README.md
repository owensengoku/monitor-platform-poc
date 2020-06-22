## Steps


### sysctl

- add `vm.max_map_count=655360` in the end of `/etc/sysctl.conf`
- `$ sudo sysctl -p`

### Elastic Search
```
mkdir -p elasticsearch/data
mkdir -p elasticsearch/logs
chmod -R 755  elasticsearch/*
```
`$ docker run -d --name elasticsearch --user 1000 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ELASTICSEARCH_USERNAME=admin -e ELASTICSEARCH_PASSWORD=admin@123  -v /home/azureuser/elasticsearch/data/:/usr/share/elasticsearch/data/ -v /home/azureuser/elasticsearch/logs/:/usr/share/elasticsearch/logs/ docker.elastic.co/elasticsearch/elasticsearch:6.5.2
`
### kibana
`$ docker run -d --name kibana -p 5601:5601 -e ELASTICSEARCH_URL=http://10.1.0.4:9200 docker.elastic.co/kibana/kibana:6.5.2`

### Logstach
`$ docker run -d --name logstash -p 5044:5044 --link elasticsearch -v /home/azureuser/logstash/logstash.conf:/usr/share/logstash/pipeline/logstash.conf docker.elastic.co/logstash/logstash:6.5.2`

### FileBeat
`$ docker run -d --name filebeat --user 1000 -v /home/azureuser/filebeat/data/:/usr/share/filebeat/data/ -v /home/azureuser/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml -v /var/log/:/var/log/ docker.elastic.co/beats/filebeat:6.5.2`

