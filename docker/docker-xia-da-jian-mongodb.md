# docker 下 搭建 mongodb

    docker-composer.yml
    
    version: '2' 
    
    services:
        mongo:
            image: mongo:3.6 
            ports: 
              - 27017:27017
            networks:
              - front-tier
              - back-tier
            volumes:
              - /data/docker-data/mongo/data:/data/db
            command: mongod --bind_ip 0.0.0.0 --auth --journal 
            container_name: mongo





    networks:
        front-tier:
            driver: bridge
        back-tier:
            driver: bridge
            
            
            
    docker-composer up -d mongo