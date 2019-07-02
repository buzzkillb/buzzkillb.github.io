---
layout: post
title: Compile Wallets easily to Spec Mine
date: {}
published: true
---
The original idea to learn to use docker was to compile and run a wallet deamon very easily. Then it became wow this is so easy why not run this for more than just staking [Denarius](https://denarius.io).  

After seeing just how easy the daemons were to compile and run, I realized I could cleanly run a wallet, get the address and private keys and mine to that. Which lead me to why I was trying to figure out how to get the QT compiled and running in docker.  

Why would someone want to do this? Well if you have the Dockerfile setup for a few different bitcoin forks, you can easily modify that Dockerfile template and build a wallet very fast without screwing around with your current OS and dependencies. Also this linux QT can be built in Linux, Windows or MacOS.  

So now using a few templates I can compile a wallet from source cleanly inside of its own docker container. This is extremely powerful and why I was spending so much time seeing how this works.

Examples  
[https://github.com/buzzkillb/denariusQTdocker](https://github.com/buzzkillb/denariusQTdocker)  
[https://github.com/buzzkillb/voltaQTdocker](https://github.com/buzzkillb/voltaQTdocker)

Example what the Denarius QT looks like running in Ubuntu 19.04

![denarius-qt-docker-ubuntu-disco-dingo.png]({{site.baseurl}}/_posts/denarius-qt-docker-ubuntu-disco-dingo.png)
