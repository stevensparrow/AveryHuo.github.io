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

### Twisted架构概览
Twisted是一个事件驱动型的网络引擎。由于事件驱动编程模型在Twisted的设计哲学中占有重要的地位，因此这里有必要花点时间来回顾一下究竟事件驱动意味着什么。

事件驱动编程是一种编程范式，这里程序的执行流由外部事件来决定。它的特点是包含一个事件循环，当外部事件发生时使用回调机制来触发相应的处理。另外两种常见的编程范式是（单线程）同步以及多线程编程。

在单线程同步模型中，任务按照顺序执行。如果某个任务因为I/O而阻塞，其他所有的任务都必须等待，直到它完成之后它们才能依次执行。这种明确的执行顺序和串行化处理的行为是很容易推断得出的。如果任务之间并没有互相依赖的关系，但仍然需要互相等待的话这就使得程序不必要的降低了运行速度。

在多线程版本中，这3个任务分别在独立的线程中执行。这些线程由操作系统来管理，在多处理器系统上可以并行处理，或者在单处理器系统上交错执行。这使得当某个线程阻塞在某个资源的同时其他线程得以继续执行。与完成类似功能的同步程序相比，这种方式更有效率，但程序员必须写代码来保护共享资源，防止其被多个线程同时访问。多线程程序更加难以推断，因为这类程序不得不通过线程同步机制如锁、可重入函数、线程局部存储或者其他机制来处理线程安全问题，如果实现不当就会导致出现微妙且令人痛不欲生的bug。

在事件驱动版本的程序中，3个任务**交错执行**，但仍然在一个单独的线程控制中。当处理I/O或者其他昂贵的操作时，注册一个回调到事件循环中，然后当I/O操作完成时继续执行。回调描述了该如何处理某个事件。事件循环轮询所有的事件，当事件到来时将它们分配给等待处理事件的回调函数。这种方式让程序尽可能的得以执行而不需要用到额外的线程。事件驱动型程序比多线程程序更容易推断出行为，因为程序员不需要关心线程安全问题。

当我们面对如下的环境时，事件驱动模型通常是一个好的选择：

程序中有许多任务，而且…
1. 任务之间高度独立（因此它们不需要互相通信，或者等待彼此）而且…
2. 在等待事件到来时，某些任务会阻塞。
3. 当应用程序需要在任务间共享可变的数据时，这也是一个不错的选择，因为这里不需要采用同步处理。

网络应用程序通常都有上述这些特点，这使得它们能够很好的契合事件驱动编程模型。

###### **重用已有的应用**
在Twisted创建之前就已经有了许多针对多种流行的网络协议的客户端和服务器实现了。为什么Glyph不直接用Apache、IRCd、BIND、OpenSSH或者任何其他已有的应用，而要为Twisted从头开始重新实现各个协议的客户端和服务器呢？

问题在于所有这些已有的实现都存在有从头写起的网络层代码，通常都是C代码。而应用层代码直接同网络层耦合在一起，这使得它们非常难以以库的形式来复用。当要一起使用这些组件时，如果希望在多个协议中暴露相同的数据，则它们必须以黑盒的形式来看待，这使得开发者根本没机会重用代码。此外，服务器和客户端的实现通常是分离的，彼此之间不共享代码。要扩展这些应用，维护跨平台的客户端-服务器兼容性的难度本不至于这么大。

Twisted中的客户端和服务器是用Python开发的，采用了一致性的接口。这使得开发新的客户端和服务器变得很容易实现，可以在客户端和服务器之间共享代码，在协议之间共享应用逻辑，以及对某个实现的代码做测试。

###### **React模式**
Twisted实现了设计模式中的反应堆（reactor）模式，这种模式在单线程环境中调度多个事件源产生的事件到它们各自的事件处理例程中去。

Twisted的核心就是reactor事件循环。Reactor可以感知网络、文件系统以及定时器事件。它等待然后处理这些事件，从特定于平台的行为中抽象出来，并提供统一的接口，使得在网络协议栈的任何位置对事件做出响应都变得简单。

基本上reactor完成的任务就是：
```
while True:
    timeout = time_until_next_timed_event()
    events = wait_for_events(timeout)
    events += timed_events_until(now())
    for event in events:
        event.process()
```