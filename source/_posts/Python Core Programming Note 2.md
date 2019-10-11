---
title: Python Core Programming Note 2
tags: 新建,模板,小书匠
---

## Net Programming

#### 1. TCP
+ Server:
```
from socket import *
from time import ctime

HOST = ''
PORT = 21111
BUFSIZ = 1024
ADDR = (HOST, PORT)

tcpSerSocket = socket(AF_INET, SOCK_STREAM)
tcpSerSocket.bind(ADDR)
tcpSerSocket.listen(5)

try:
    while True:
        print("waiting for connection...")
        tcpCliSocket, addr = tcpSerSocket.accept()
        print("connected from :",addr)

        while True:
            data = tcpCliSocket.recv(BUFSIZ)
            if not data:
                break
            print("rec:",data)
            send_str = '[%s] %s' %(bytes(ctime(), 'utf-8'), 'Oh?')
            tcpCliSocket.send(send_str.encode('utf-8'))
            
        tcpCliSocket.close()
except EOFError:
    print("Error: EOFEError")
except KeyboardInterrupt:
    print("Error: EOFEError")
finally:
    tcpSerSocket.close()


```

#### 2. UDP

