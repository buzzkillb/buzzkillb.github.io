---
published: true
---
## Docker TOR and a Bunch of Containers

Playing around with the [Denarius](https://denarius.io) wallet daemon and really wanted to run denariusd wallet, tor, and electrumx under docker. But its a bit of a pain to run electrumx as the server needs to compact history at least every 2 weeks. I also wanted to run tor without installing anything so this node could also act as an onion node with hidden services. Maybe eventually turning the electrumx server into an onion server as well if people want that.  

So basically run docker tor I made. I made a debian slim version under latest branch or alpine version under alpine branch.  [https://github.com/buzzkillb/dockertor](https://github.com/buzzkillb/dockertor)  

```
docker run -d --name tor --net host -v /etc/tor/torrc:/etc/tor/torrc buzzkillb/tor:alpine
```
Then run denariusd  
```
docker run \
  --net=host \
  --name=denariusd \
  -t -d \
  -p 33369:33369 \
  -p 32369:32369 \
  -v ~/.denarius:/data \
  -P buzzkillb/denariusd:latest
```

Then run electrumx after fully syncing.  
```
docker run \
  --name=electrumx \
  --net=host \
  --ulimit nofile=5120:5120 \
  -t -d \
  -v ~/electrumx:/data \
  -e DAEMON_URL=http://denariusrpc:PASSWORDFROMDENARIUS.CONF@127.0.01:32369 \
  -e COIN=Denarius \
  -p 50001:50001 \
  -p 50002:50002 \
  buzzkillb/docker-electrumx:latest
```

Then stop electrumx and run the compaction once.   
```
docker run \
  --name=electrumx-compact \
  --net=host \
  --ulimit nofile=5120:5120 \
  -t -d \
  -v ~/electrumx:/data \
  -e DAEMON_URL=http://denariusrpc:RPCPASSWORD@127.0.01:32369 \
  -e COIN=Denarius \
  -p 50002:50002 \
  buzzkillb/docker-electrumx:dcompact
```

Then restart electrumx server. And like that its all setup. Then make a crontab like so.  
```
0 0 * * * docker stop electrumx >/dev/null 2>&1
1 0 * * * docker start electrumx-compact >/dev/null 2>&1
6 0 * * * docker start electrumx >/dev/null 2>&1
```

And you now have an electrumx server running denariusd as an onion node. The above steps can be forked, tweaked and able to run on whatever bitcoin fork.  

reference - [ElectrumX Server Setup Guide [Docker]](https://denariustalk.org/index.php?/topic/282-electrumx-server-setup-guide-docker/)
