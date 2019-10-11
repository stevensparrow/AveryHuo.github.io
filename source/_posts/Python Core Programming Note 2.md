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
+ Client
```
from socket import *

HOST = '127.0.0.1' 
PORT = 21111
BUFSIZ = 1024
ADDR = (HOST, PORT)

tcpCliSocket = socket(AF_INET, SOCK_STREAM)
tcpCliSocket.connect(ADDR)

while True:
    data = input('> ')
    if not data:
        break

    tcpCliSocket.send(data.encode('utf-8'))
    data = tcpCliSocket.recv(BUFSIZ)
    if not data:
        break
    print(data.decode('utf-8'))

tcpCliSocket.close()

```

#### 2. UDP

+ Server
```
from socket import *
from time import ctime

HOST = ''
PORT = 21111
BUFSIZ = 1024
ADDR = (HOST, PORT)

udpSerSocket = socket(AF_INET, SOCK_DGRAM)
udpSerSocket.bind(ADDR)

try:
    while True:
        print("waiting for message...")
        msg, addr = udpSerSocket.recvfrom(BUFSIZ)
        if msg.decode('utf-8') == ' ':
            break
        print('Rev client:',msg)
        send_str = '[%s] %s' %(bytes(ctime(), 'utf-8'), msg)
        udpSerSocket.sendto(send_str.encode('utf-8'),addr)
        
except EOFError:
    print("Error: EOFEError")
except KeyboardInterrupt:
    print("Error: EOFEError")
finally:
    udpSerSocket.close()


```
+ Client
```
from socket import *

HOST = '127.0.0.1' 
PORT = 21111
BUFSIZ = 1024
ADDR = (HOST, PORT)

udpCliSocket = socket(AF_INET, SOCK_DGRAM)
while True:
    data = input('> ')
    if not data:
        break

    udpCliSocket.sendto(data.encode('utf-8'),ADDR)
    if data == ' ':
        break
    data,ADDR = udpCliSocket.recvfrom(BUFSIZ)
    if not data:
        break
    print(data.decode('utf-8'))

udpCliSocket.close()
```

### 使用SocketServer
+ Server
```
from socketserver import (TCPServer as TCP, StreamRequestHandler as SRH)
from time import ctime


HOST = ''
PORT = 21111
BUFSIZ = 1024
ADDR = (HOST, PORT)

class MyRequestHandler(SRH):
    def handle(self):
        print("connected from..", self.client_address)
        send_str = '[%s] %s' %(bytes(ctime(), 'utf-8'), self.rfile.readline())
        self.wfile.write(send_str.encode('utf-8'))

tcpServ = TCP(ADDR, MyRequestHandler)
print("waiting for connection...")
tcpServ.serve_forever()
        
```
+ Client
不同之处：需要把建立和连接放在每次循环中
```
from socket import *

HOST = '127.0.0.1' 
PORT = 21111
BUFSIZ = 1024
ADDR = (HOST, PORT)



while True:
    tcpCliSocket = socket(AF_INET, SOCK_STREAM)
    tcpCliSocket.connect(ADDR)
    data = input('> ')
    if not data:
        break

    send_data = "%s\n" % data
    tcpCliSocket.send(send_data.encode('utf-8'))
    data = tcpCliSocket.recv(BUFSIZ)
    if not data:
        break
    print(data.decode('utf-8'))
    tcpCliSocket.close()

```

## Twisted


### Python Twisted介绍
Twisted是用Python实现的基于事件驱动的网络引擎框架。Twisted诞生于2000年初，在当时的网络游戏开发者看来，无论他们使用哪种语言，手中都鲜有可兼顾扩展性及跨平台的网络库。Twisted的作者试图在当时现有的环境下开发游戏，这一步走的非常艰难，他们迫切地需要一个可扩展性高、基于事件驱动、跨平台的网络开发框架，为此他们决定自己实现一个，并从那些之前的游戏和网络应用程序的开发者中学习，汲取他们的经验教训。

Twisted支持许多常见的传输及应用层协议，包括TCP、UDP、SSL/TLS、HTTP、IMAP、SSH、IRC以及FTP。就像python一样，Twisted也具有“内置电池”（batteries-included）的特点。Twisted对于其支持的所有协议都带有客户端和服务器实现，同时附带有基于命令行的工具，使得配置和部署产品级的Twisted应用变得非常方便。

### 为什么需要Twisted
2000年时，Twisted的作者Glyph正在开发一个名为Twisted Reality的基于文本方式的多人在线游戏。这个游戏采用Java开发，里面尽是一堆线程——每个连接就有3个线程处理。处理输入的线程会在读操作上阻塞，处理输出的线程将在一些写操作上阻塞，还有一个“逻辑”线程将在等待定时器超时或者事件入队列时休眠。随着玩家们在虚拟世界中移动并交互时，线程出现死锁，缓存被污染，程序中的加锁逻辑几乎从来就没对过——采用多线程使得整个软件变得复杂、漏洞百出而且极难扩展。

为了寻求其他的解决方案，作者发现了Python，特别是Python中用于对流式对象比如socket和pipe进行多路I/O复用的select模块（UNIX规范第3版（SUSv3）描述了select）。那时，Java并没有提供操作系统的select接口或者任何其他的异步I/O API（针对非阻塞式I/O的包java.nio已经在J2SE 1.4中加入了，2002年发布）。通过用Python中的select模块快速搭建起游戏的原型，这迅速降低了程序的复杂度，并且比多线程版本要更加可靠。

Glyph迅速转向了Python、select以及基于事件驱动的编程。他使用Python的select模块为游戏编写了客户端和服务器。但他想要的还不止于此。从根本上说，他希望能将网络行为转变为对游戏中的对象的方法调用。如果你能在游戏中收取邮件会怎样，就像Nethack mailer这种守护进程一样？如果游戏中的每位玩家都拥有一个主页呢？Glyph发现他需要优秀的IMAP以及HTTP客户端和服务器的Python实现，而这些都要采用select。

他首先转向了Medusa，这是一个在90年代中期开发的平台，在这里可以采用Python中的asyncore模块来编写网络服务。asyncore是一个异步化处理socket的模块，在操作系统的select API之上构建了一个调度器和回调接口。

这对于Glyph来说是个激动人心的发现，但Medusa有两个缺点：
1. 这个项目到2001年就不再维护了，那正是glyph开发Twisted Reality的时候。
2. asyncore只是对socket的一个薄封装层，应用程序的编写者仍然需要直接操作socket。这意味着程序可移植性的担子仍然落在程序员自己身上。此外，那时asyncore对Windows的支持还有问题，Glyph希望能在Windows上运行一个带有图形用户界面的客户端。
Glyph需要自己实现一个网络引擎平台，而且他意识到Twisted Reality已经打开了问题的大门，这和他的游戏一样有趣。

随着时间的推移，Twisted Reality这个游戏就演化成了Twisted网络引擎平台。它可以做到当时Python中已有的网络平台所无法做到的事情：
+ 使用基于事件驱动的编程模型，而不是多线程模型。
+ 跨平台：为主流操作系统平台暴露出的事件通知系统提供统一的接口。
+ “内置电池”的能力：提供流行的应用层协议实现，因此Twisted马上就可为开发人员所用。
+ 符合RFC规范，已经通过健壮的测试套件证明了其一致性。
+ 能很容易的配合多个网络协议一起使用。
+ 可扩展。