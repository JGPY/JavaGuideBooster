# Socket 编程
### 目录

---
<a href="#1">1. socket 编程的基本步骤(TCP/UDP)。</a> <br>
<a href="#2">2. Socket 通信模型。</a> <br>
<a href="#3">3. Socket I/O模型。</a> <br>

### <a name="1">1. socket 编程的基本步骤(TCP/UDP)。</a>
&ensp;&ensp;&ensp;&ensp;
    创建 Socket 连接时,可以指定使用的传输层协议,Socket 可以支持不同的传输层协
议(TCP 或 UDP),当使用 TCP 协议进行连接时,该 Socket 连接就是一个 TCP 连接。
Server 端所要做的事情主要是建立一个通信的端点,然后等待客户端发送的请求。典型的
处理步骤如下:(服务器端建立连接过程) <br>
1. 构建一个 ServerSocket 实例,指定本地的端口。这个 socket 就是用来监听指定端口的
连接请求的。 <br>
2.重复如下几个步骤: <br>
- a. 调用 socket 的 accept()方法来获得下面客户端的连接请求。通过 accept()方法返回的socket 实例,建立了一个和客户端的新连接。
- b.通过这个返回的 socket 实例获取 InputStream 和 OutputStream,可以通过这两个 stream来分别读和写数据。
- c.结束的时候调用 socket 实例的 close()方法关闭 socket 连接。

客户端的请求过程稍微有点不一样: <br>
1.构建 Socket 实例,通过指定的远程服务器地址和端口来建立连接。 <br>
2.通过 Socket 实例包含的 InputStream 和 OutputStream 来进行数据的读写。 <br>
3.操作结束后调用 socket 实例的 close 方法,关闭。 <br>

#### 简单的 Client/Server 程序设计

服务端
```java
import java.io.*;
import java.net.*;
public class Service {
    public static void main(String args[]) {
        try {
            ServerSocket server = null;
            try {
                server = new ServerSocket(4700);// 创建一个 ServerSocket 在端口 4700 监听客户请求
            } catch (Exception e) {
                System.out.println("can not listen to:" + e);// 出错,打印出错信息
            }
            System.out.println("server------------------------------");
            Socket socket = null;
            try {
                socket = server.accept();// 使用 accept()阻塞等待客户请求,有客户
                // 请求到来则产生一个 Socket 对象,并继续执行
            } catch (Exception e) {
                System.out.println("Error." + e);// 出错,打印出错信息
            }
            String line;
            BufferedReader is = new BufferedReader(new InputStreamReader(socket.getInputStream()));// 由 Socket 对象得到输入流,并构造相应的 BufferedReader 对象
            PrintWriter os = new PrintWriter(socket.getOutputStream());// 由 Socket 对象得到输出流,并构造 PrintWriter 对象
            BufferedReader sin = new BufferedReader(new InputStreamReader(System.in));// 由系统标准输入设备构造 BufferedReader 对象
            System.out.println("Client:" + is.readLine());// 在标准输出上打印从客户端读入的字符串
            line = sin.readLine();// 从标准输入读入一字符串
            while (!line.equals("bye")) {// 如果该字符串为 "bye",则停止循环
                // 向客户端输出该字符串
                os.println(line);
                // 刷新输出流,使 Client 马上收到该字符串
                os.flush();
                // 从 Client 读入一字符串,并打印到标准输出上
                System.out.println("Client:" + is.readLine()+"\n");
                line = sin.readLine();// 从系统标准输入读入一字符串
            } // 继续循环
            os.close(); // 关闭 Socket 输出流
            is.close(); // 关闭 Socket 输入流
            socket.close(); // 关闭 Socket
            server.close(); // 关闭 ServerSocket
        } catch (Exception e) {
            System.out.println("Error:" + e);// 出错,打印出错信息
        }
    }
}
```

客户端
```java
import java.io.*;
import java.net.*;
public class Client {
    public static void main(String args[]) {
        try {
            Socket socket = new Socket("127.0.0.1",4700);// 向本机的 4700 端口发出客户请求
            BufferedReader sin = new BufferedReader(new InputStreamReader(System.in));// 由系统标准输入设备构造 BufferedReader 对象
            PrintWriter os = new PrintWriter(socket.getOutputStream());// 由 Socket 对象得到输出流,并构造 PrintWriter 对象
            BufferedReader is = new BufferedReader(newInputStreamReader(socket.getInputStream()));
            System.out.println("Client------------------------------");// 由 Socket 对象得到输入流,并构造相应的 BufferedReader 对象
            String readline;
            readline = sin.readLine(); // 从系统标准输入读入一字符串
            while (!readline.equals("bye")) {// 若从标准输入读入的字符串为 "bye"则停止循环
                os.println(readline);
                // 将从系统标准输入读入的字符串输出到 Server
                os.flush();
                // 刷新输出流,使 Server 马上收到该字符串
                System.out.println("Server:" + is.readLine());
                // 从 Server 读入一字符串,并打印到标准输出上
                readline = sin.readLine(); // 从系统标准输入读入一字符串
            } // 继续循环
            os.close(); // 关闭 Socket 输出流
            is.close(); // 关闭 Socket 输入流
            socket.close(); //关闭 Socket
        } catch (Exception e) {
            System.out.println("Error" + e); //出错,则打印出错信息
        }
    }
}
```


### <a name="2">2. Socket 通信模型。</a>
Select 事件模型,epoll 事件模型。

#### Windows 高并发socket通信模型
&ensp;&ensp;&ensp;&ensp;
    Windows操作系统提供了选择（Select）、异步选择（WSAAsyncSelect）、事件选择（WSAEventSelect）、
重叠I/O（Overlapped I/O）和完成端口（Completion Port)共五种I/O模型。 <br>

#### linux 高并发socket通信模型
------select

1 一个误区很多人认为它最大可以监听1024个，实际上却是文件描述符的值不能大于等于1024，所以除掉标准输入、输出、错误输出，
一定少于1024个，如果在之前还打开了其他文件，那会更少 <br>

2 select返回后，一般要轮询fd_set，发现新连接要加上，连接断开要去掉，这个过程一定要这样做：select之前把fd_set临时拷贝一份，
轮询中对它的修改只在临时fd_set上做，轮询完了，再对这个临时fd_set select，否则你可能明明有连接进来，却accept不到，这可能是
因为轮询中如果直接修改fdset，select的底层就会定位错乱 <br>


------poll
&ensp;&ensp;&ensp;&ensp;
    性能测试发现，select与poll有相似的调用时间与cpu占用率，都随着数据量变大或者连接数变大（活动连接不变）而变大
连接进入时，返回POLLIN，连接关闭时返回POLLERR 或者 POLLIN <br>


------epoll
&ensp;&ensp;&ensp;&ensp;
    正如传说的那样，epoll的调用时间与cpu占用率只会随数据量变大，而几乎不受连接数影响。当连接关闭时，会收到EPOLLIN事件。
在ET模式下，不管是监听socket还是连接客户端的socket，在EPOLLIN时，都应该重复read一直到EAGAIN（多次连接进入或者客户端的
多次send调用都只产生一次EPOLL事件），否则下次等待EPOLLIN将会挂起，这样对上层应用处理起来更复杂，所以还是推荐用默认的LT模式。
在对客户端的发送也可能出现阻塞，所以epoll也应该注册EPOLLOUT，但不是在一开始（那会让所有文件描述符都返回可用，降低epoll的效率，
合理的机制应该是这样：对accecpt的客户端连接一开始只注册EPOLLIN事件，触发后接收客户端消息，生成回复，将回复放到一个程序自己的缓冲区内，
修改该文件描述符的注册事件为EPOLLIN|EPOLLOUT（视业务逻辑而定，如果要求必须应答发送之前不能接收请求，可只注册EPOLLOUT事件），
当EPOLLOUT触发时，将回复发送出去，从缓冲区中删除回复，再修改该连接为注册EPOLLIN事件。即使在单线程程序中（运行在家用笔记本的虚拟机上），
在3万个连接的1万个活动连接上，epoll也可以一秒内收发100MB数据（已经接近于Gbit网卡的理论上限），所以如果没有其它的IO活动或者计算处理，
单线程的epoll完全可以应付高并发socket通信。如果连接爆发，比如一秒1万个，epoll server会在10+秒内accept完，没必要担心它accept过慢，
因为当监听队列不足时，tcp会忽略客户端的SYN报文，这样客户端就会重传，只要给客户端设置一个合适的超时时间，例如15妙，epoll server处理每秒10000个新加连接没有问题


-----一般处理模型
&ensp;&ensp;&ensp;&ensp;
    生产者消费者模式，一个线程单独负责从监听socket上accept，它收到新连接后，加锁放入公共buffer，若干个工作线程加锁从公共buffer上取得连接，
加入自己的epoll等待集中，等待一定的时间，有数据则进行收发，没数据继续从公共buffer上取连接，但是这里并不适用在线程间用条件变量通知，
因为即使公共buffer上没有新连接，工作线程也不应该等待accept线程通知，而是应立即用epoll wait自己已有的连接。

不能采用多个线程自主抢占连接的方式，数据在不同连接上是不均匀的，如果一些连接现在数据量现在过大，就会得到很少的新连接，以后又会出现数据饥饿，
而那些当时抢占到过多连接的线程以后则会压力过大，处理变慢。应该由单独线程，例如负责accept的线程，分配到每个线程自己的连接队列中等待处理，
另外，每个处理线程都采用LT模式，每个活动连接上轮流接收一次消息，然后就取回队列中的新连接，如果采用ET模式，就可能一直忙于在旧连接上收发数据，而冷落新连接。

公司的网络备份软件，采用的是poll/select模型，因为客户端一旦运行备份/恢复任务，在连接就一定有数据收发任务，这种情况下，epoll不能加快性能。
对于某些输入io只有一路的程序，数据接收线程 + circle buffer + 数据处理线程是一个比较简单的模型。

上面的方案仍然造成数据量的线程处理不过来，数据量小的线程又很空闲，应该采用如下方案 <br>
    主线程内用epoll接收数据和accept新连接，并解析出消息，放入队列中让所有的线程去抢，至于如何多个线程同时对一个连接发送消息，
可以采用与dedupe中多线程处理FP cache（一个hash table）的方案类似，分配与线程数目相同的锁，当处理完消息需要发送时，将连
接的文件描述符数除以线程数目，余是多少，就加锁哪个锁，这样，多个线程能尽量分配到不同的锁上增加并发性，而对同一个连接加同一
个锁进行互斥的发送。另外，这还需要处理SIGPIPE消息，以免前面一个线程关闭了连接，另一个线程又去发送，产生SIGPIPE信号，使进程exit


### <a name="3">3. Socket I/O模型。</a>
- 1)阻塞I/O（blocking I/O）
- 2)非阻塞I/O （nonblocking I/O）
- 3)I/O复用(select 和poll) （I/O multiplexing）
- 4)信号驱动I/O （signal driven I/O (SIGIO)）
- 5)异步I/O （asynchronous I/O (the POSIX aio_functions)）

前四种都是同步，只有最后一种才是异步IO。
[详细链接](https://blog.csdn.net/taiyang1987912/article/details/43731629)

---
### 搬运工信息
Author:Jason Lou <br>
Email:vip.iotworld@gmail.com <br>
Blog:https://blog.csdn.net/qq_21508727 <br>
Github:https://github.com/JGPY/JavaGuideBooster <br>
---
