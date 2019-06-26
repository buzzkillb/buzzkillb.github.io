---
layout: post
title: "Docker Daemon RPC Connect"
date: 2019-06-25
---

This one threw me for a loop. How to RPC connect to a dockerized wallet daemon. I came across so many people asking how to do this for Bitcoin, yet I found no responses besides put rpcallowip=* in the bitcoin.conf. The coin I was testing this on does not allow the * in that field. Of course.  

I tried many different combinations of ip's. localhost, 192.blah.bleh, 127.blah.bleh. Then thought what happens if I try the local docker container ipv4? Took me a few tries, but it was a combination of different ipv4's I came across.  
```
rpcallowip=172.19.0.0/0
```
This ended up being the trick. With samples below and reference to docker file where I was playing around with this.  
Sample docker-compose.yml  
```
version: "3"
services:
  volta:
    image: buzzkillb/voltad:latest
    volumes:
      - ~/.volta:/data
    ports:
      - 14143:14143
      - 13143:13143
  explorer:
    build: ./explorer
    stdin_open: true
    tty: true
    ports:
      - 3001:3001
    links:
      - mongodb
      - volta
    depends_on:
      - mongodb
      - volta
    command: /bin/bash -c "service cron start && cd /opt/iquidus && npm start"
  mongodb:
    image: mongo:latest
    container_name: "mongodb"
    environment:
      - MONGO_DATA_DIR=/data/db
      - MONGO_LOG_DIR=/dev/null
    volumes:
      - ./data/db:/data/db
    ports:
      - 27017:27017
    command: mongod --smallfiles --bind_ip 0.0.0.0 --logpath=/dev/null --quiet
```
sample .conf  
```
port=14143
rpcport=13143
server=1
rpcuser=RPCUSERNAME
rpcpassword=PASSWORDCHANGEME
txindex=1
listen=1
rpcallowip=172.19.0.0/0
```
reference post - [buzzkillb/iquidusdocker](https://github.com/buzzkillb/iquidusdocker) 
