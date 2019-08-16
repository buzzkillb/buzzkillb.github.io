---
layout: post
title: "Raspberry Pi 4 Docker and Docker Compose"
date: 2019-08-15
---

Just got the Raspberry PI4 4gb today and went looking for how to install docker and docker-compose on the new toy. Appears that Raspbian Buster does not play well with these just yet.
  
Docker  
```
curl -sL get.docker.com | sed 's/9)/10)/' | sh
```

Docker-compose  
```
sudo apt-get install build-essential libssl-dev libffi-dev python3-dev python3-pip
sudo pip3 install cryptography
sudo pip3 install docker-compose
docker-compose --version
```
