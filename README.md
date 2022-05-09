# f2pconn
------
## Feature

1. tranform  miner stratum to plugin proxy to pool
2. alter message by lark or dingding webhook
```
Usage of ./minerProxy_xxx:
         ./minerAgent_xxxx
  -service string
      "start", "stop", "restart", "install", "uninstall", "status"
```
Configuration instructions：

minerAgent_xxxx.yaml   
```
level: info
apiserver: 0.0.0.0:19999
server:
    eth:
        crt: ""
        key: ""
        ports:
            0.0.0.0:8888: tcp
            0.0.0.0:8889: tls
        local:
            # remote rpc addrss
            xxxx: udp
        
alert: 
    lark:
        url: ""
        sign: ""
        msg: ""
    ding:
        url: ""
        sign: ""
        msg: ""           
```

minerProxy_xxx.yaml  
```
level: warn
apiserver: 0.0.0.0:19999
server:
    eth:
        ports:
            0.0.0.0:8888: udp
        remote: 
            "eth.f2pool.com:6688": "tcp"
        crt: ""
        key: ""
```

Api:
```
 curl 127.0.0.1/show 
 will generate default configuration like minerProxy_xxx.yaml

 curl 127.0.0.1/status
 will show connect msg
```
enjoy yourself :)
 
