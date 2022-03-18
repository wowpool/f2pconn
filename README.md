# f2pconn
------
## Feature

1. tranform  miner stratum to plugin proxy to pool 

2. alter message by lark or dingding webhook

## start 
```
Usage of ./minerProxy_xxx:
         ./minerAgent_xxxx
  -service string
      "start", "stop", "restart", "install", "uninstall", "status"
```
## Configuration instructions：

minerAgent_xxxx.yaml   
```
apiserver: 0.0.0.0:19999 # ctrl api 
subscribe: false  #  use f2p self proxy
alert:    
  lark:    #lark  bot  https://www.feishu.cn/hc/zh-CN/articles/360024984973
  sign:    # lark sign if used  
  dinging: # dingding bot https://www.dingtalk.com/qidian/help-detail-20781541.html
  msg: "has been" #  message profix
server:
    eth:
        connsize: 1
        # crt:  cert.pem # Some miners need to be certified for certificates that need to be filled in
        # key:   key.pem # Some miners need to be certified for certificates that need to be filled in
        ports:
            "0.0.0.0:8888": tcp
            "0.0.0.0:8889": tls
        local:   ##Custom proxy address, plug-in stream has rpc and udp to choose, udp delay will be low
            "hk-f2.wowpool.com:10000": udp
            
```

minerProxy_xxx.yaml  
```
apiserver: "0.0.0.0:19998"
server:
    eth:
        limit:  6000  #second
        # crt:  cert.pem
        # key:    key.pem
        ports:
          "0.0.0.0:8888": "tls" #  miner stratum
          "0.0.0.0:10000":  "udp" # agent 
        remote:
          "eth.f2pool.com:6688": "tcp"
```

Api:
```
 curl 127.0.0.1/show 
 will generate default configuration like minerProxy_xxx.yaml

 curl 127.0.0.1/status
 will show connect msg
```


-----------
  You can run the program directly to test network connectivity.
  After the test is successful, install it as a service

 1~2% loss may be caused due to network problems and delays
 
