```yml
version: '2.2'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:6.3.0
    container_name: elasticsearch
    environment:
      - cluster.name=docker-cluster
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - /home/web/docker_data/elasticsearch/data/1:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - esnet
    user: "1000"

  elasticsearch2:
    image: docker.elastic.co/elasticsearch/elasticsearch:6.3.0
    container_name: elasticsearch2
    environment:
      - cluster.name=docker-cluster
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - "discovery.zen.ping.unicast.hosts=elasticsearch"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - /home/web/docker_data/elasticsearch/data/2:/usr/share/elasticsearch/data
    networks:
      - esnet
    user: "1000"

  kibana:
    image: docker.elastic.co/kibana/kibana:6.3.0
    container_name: kibana
    volumes:
      - /home/web/docker_data/elasticsearch/data/kibana/config/kibana.yml:/usr/share/kibana/config/kibana.yml
    ports:
      - 5601:5601
    networks:
      - esnet

volumes:
  esdata1:
    driver: local
  esdata2:
    driver: local

networks:
  esnet:
    driver: bridge
```
