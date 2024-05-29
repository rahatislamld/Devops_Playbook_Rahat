# Docker Compose Configuration for ELK Stack

This Docker Compose configuration sets up the ELK (Elasticsearch, Logstash, Kibana) Stack using Docker containers.

## Prerequisites

- Docker installed on your machine.

## Services

### Elasticsearch

```yaml
version: "3"
services:
  elasticsearch:
    image: elasticsearch:7.9.1
    container_name: elasticsearch
    ports:
      - "9200:9200"
      - "9300:9300"
    volumes:
      - test_data:/usr/share/elasticsearch/data/
      - ./elk-config/elasticsearch/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml
    environment:
      - discovery.type=single-node
      - http.host=0.0.0.0
      - transport.host=0.0.0.0
      - xpack.security.enabled=false
      - xpack.monitoring.enabled=false
      - cluster.name=elasticsearch
      - bootstrap.memory_lock=true
    networks:
      - elk

  logstash:
    image: logstash:7.9.1
    container_name: logstash
    ports:
      - "5044:5044"
      - "9600:9600"
    volumes:
      - ./elk-config/logstash/logstash.conf:/usr/share/logstash/pipeline/logstash.conf
      - ./elk-config/logstash/logstash.yml:/usr/share/logstash/config/logstash.yml
      - ls_data:/usr/share/logstash/data

    networks:
      - elk
    depends_on:
      - elasticsearch

  kibana:
    image: kibana:7.9.1
    container_name: kibana
    ports:
      - "5601:5601"
    volumes:
      - ./elk-config/kibana/kibana.yml:/usr/share/kibana/config/kibana.yml
      - kb_data:/usr/share/kibana/data
    networks:
      - elk
    depends_on:
      - elasticsearch

networks:
  elk:
    driver: bridge

volumes:
  test_data:
  ls_data:
  kb_data:
```

## elk_config_files

elastic_config

```
cluster.name: "elasticsearch"
network.host: localhost
```

kibana_config

```
# Default Kibana configuration for docker target
server.name: kibana
server.host: "0"
elasticsearch.hosts: ["http://elasticsearch:9200"]
monitoring.ui.container.elasticsearch.enabled: true
```

logtash_config

```
input {
   beats{
   port => 5044
   }
}

filter {
}

output {
   elasticsearch {
   hosts => "http://elasticsearch:9200"
   index => "filebeat-test%{+YYYY.MM.DD}"
   user => "elastic"
   password => "password"
 }
}
```

logtash.yml

```
http.host: 0.0.0.0
xpack.monitoring.elasticsearch.hosts: ["http://elasticsearch:9200"]
```

## Accessing ELK Stack

After bringing up the ELK Stack with Docker Compose, you can access the services as follows:

### Elasticsearch

Elasticsearch is accessible via HTTP on port 9200. You can use tools like curl or a web browser to interact with it:
http://localhost:9200

### Kibana

Kibana is accessible via HTTP on port 5601. Open your web browser and navigate to the following address:
http://localhost:5601

### Logstash

Logstash is primarily used for log processing and forwarding, and typically doesn't have a direct user interface. However, you can access its monitoring and management API on port 9600:
http://localhost:9600
