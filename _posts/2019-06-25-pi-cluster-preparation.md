---
layout: post
title: "Raspberry Pi 4 Cluster Preparing"
date: 2019-06-25
---

With the release of the [raspberry pi4](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/) and 4gb of ram, I am now curious about running multi masternodes on kubernetes or docker swarm.  
Seeing people post images of cluster setups I thought there were already boards made to run a bunch of raspberry pi's. Wrong! Everyone is tinkering away at creating their own very custom setups.  
I am attempting to replace a 16core threadripper 2950 with 96gb of ram, and use 20-24 pi4's to see if that is possibe to save a bit on power, and then bring the Threadripper to becoming my Main PC.  
From what I can figure out I will need a 24 port switch, 20 pi4's, 20 ethernet cables, 1tb ssd, and a 20port USB powered hub.  
What I plan to do as a test is get 2-3 raspberry pi4's, and put them in a docker swarm and just keep adding wallet daemons until the thing grinds to a halt and then see where things break and what is needed. Will I be core starved? Probably not. But I may be ram starved for what I am planning on doing.
