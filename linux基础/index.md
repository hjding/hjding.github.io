# linux基础


## linux环境变量

/etc/profile，/etc/bashrc 是系统全局环境变量设定

/.profile，/.bashrc用户家目录下的私有环境变量设定

当登入系统时候获得一个shell进程时，其读取环境设定档有三步
1. 首先读入的是全局环境变量设定档/etc/profile，然后根据其内容读取额外的设定的文档，如
/etc/profile.d和/etc/inputrc
2. 然后根据不同使用者帐号，去其家目录读取~/.bash_profile，如果这读取不了就读取~/.bash_login，这个也读取不了才会读取~/.profile，这三个文档设定基本上是一样的，读取有优先关系
3. 然后在根据用户帐号读取~/.bashrc

### /.profile与/.bashrc的区别

都具有个性化定制功能
~/.profile可以设定本用户专有的路径，环境变量等，它只能登入的时候执行一次
~/.bashrc也是某用户专有设定文档，可以设定路径，命令别名，每次shell script的执行都会使用它一次

## linux下.so、.ko、.a、.o的区别

各类文件的区别与作用：
1、对于.so文件
.so文件是用户层的动态链接库，用于用户层的动态链接使用，内核态的代码同样不能直接访问。
2、对于.ko文件
.ko文件是内核态的动态链接库，用于内核态的动态链接使用，可以用于内核之间的模块相互调用。用户态的代码不可直接调用内核态的代码，但是可以通过其他方式进行通信。
3、对于.a文件
.a文件是用于静态链接时，使用的静态库。
4、对于.o文件
.o文件是目标文件，编译生成，.a文件就是由.o文件打包生成的。

## linux源码编译

有时候需要手动安装各种依赖库，注意安装选项

```
mkdir build; cd build 
cmake .. 
make 
make install
```



## linux进程空间

栈stack低地址增长，堆heap高地址增长

![](..\images\3_linux进程空间.png)

程序段(Text):程序代码在内存中的映射，存放函数体的二进制代码。
初始化过的数据(Data):在程序运行初已经对变量进行初始化的数据。
未初始化过的数据(BSS):在程序运行初未对变量进行初始化的数据。
栈 (Stack):存储局部、临时变量，函数调用时，存储函数的返回指针，用于控制函数的调用和返回。在程序块开始时自动分配内存,结束时自动释放内存，其操作方式类似于数据结构中的栈。
堆 (Heap):存储动态内存分配,需要程序员手工分配,手工释放.注意它与数据结构中的堆是两回事，分配方式类似于链表。
注：
1.Text, BSS, Data段在编译时已经决定了进程将占用多少VM可以通过size，知道这些信息；

2. 正常情况下，Linux进程不能对用来存放程序代码的内存区域执行写操作，即程序代码是以只读的方式加载到内存中，但它可以被多个进程安全的共享。

### 内核空间和用户空间

Linux的虚拟地址空间范围为0～4G，Linux内核将这4G字节的空间分为两部分，将最高的1G字节（从虚拟地址0xC0000000到0xFFFFFFFF）供内核使用，称为“内核空间”。而将较低的3G字节（从虚拟地址0x00000000到0xBFFFFFFF）供各个进程使用，称为“用户空间。因为每个进程可以通过系统调用进入内核，因此，Linux内核由系统内的所有进程共享。于是，从具体进程的角度来看，每个进程可以拥有4G字节的虚拟空间。

## socket套接字

tcp/ip协议中的backlog参数
int listen(int sockfd, int backlog); // 返回：成功返回0，出错-1

linux内核2.2之前，backlog包括syns queue和accept queue
linux内核2.2之后，syns queue由/proc/sys/net/ipv4/tcp_max_syn_backlog 指定，默认为2048；accept queue写死在代码常量 SOMAXCON， 和使用listen函数时传入的backlog参数，二者取最小值。默认为128
linux内核2.4.25之后，accept queue由/proc/sys/net/core/somaxconn 和使用listen函数时传入的参数，二者取最小值，默认为128。也可/etc/sysctl.conf 中配置 net.core.somaxconn = 128



![](D:\Hugo\my_website\content\images\3_linux-socket.png)

![3_linux-tcp](D:\Hugo\my_website\content\images\3_linux-tcp.png)

![3_linux-tcp2](D:\Hugo\my_website\content\images\3_linux-tcp2.png)

![3_linux-tcp3](D:\Hugo\my_website\content\images\3_linux-tcp3.png)

![3_linux-tcp4](D:\Hugo\my_website\content\images\3_linux-tcp4.png)

### ss -l

在LISTEN状态，其中 Send-Q 即为Accept queue的最大值，Recv-Q 则表示Accept queue中等待被服务器accept()。

另外客户端connect()返回不代表TCP连接建立成功，有可能此时accept queue 已满，系统会直接丢弃后续ACK请求；客户端误以为连接已建立，开始调用等待至超时；服务器则等待ACK超时，会重传SYN+ACK 给客户端，重传次数受限 net.ipv4.tcp_synack_retries ，默认为5，表示重发5次，每次等待30~40秒，即半连接默认时间大约为180秒，该参数可以在tcp被洪水攻击是临时启用这个参数。

### 查看SYN queue 溢出

```
netstat -s | grep LISTEN
102324 SYNs to LISTEN sockets dropped
```



### 查看Accept queue 溢出

```
netstat -s | grep TCPBacklogDrop
TCPBacklogDrop: 2334
```



## k8s、docker、微服务

官方定义1：Docker是一个开源的应用容器引擎，开发者可以打包他们的应用及依赖到一个可移植的容器中，发布到流行的Linux机器上，也可实现虚拟化。
官方定义2：k8s是一个开源的容器集群管理系统，可以实现容器集群的自动化部署、自动扩缩容、维护等功能。
说白了，我们用kubernetes去管理Docker集群，即可以将Docker看成Kubernetes内部使用的低级别组件。另外，kubernetes不仅仅支持Docker，还支持Rocket，这是另一种容器技术。
站在 Docker 的角度，软件就是容器的组合：业务逻辑容器、数据库容器、储存容器、队列容器......Docker 使得软件可以拆分成若干个标准化容器，然后像搭积木一样组合起来。这正是微服务（microservices）的思想：软件把任务外包出去，让各种外部服务完成这些任务，软件本身只是底层服务的调度中心和组装层。



## linux socket

### epoll

epoll_create 创建一个epoll文件描述符
epoll_ctl 添加/修改/删除需要侦听的文件描述符及其事件
epoll_wait/epoll_pwait 接收发生在被侦听的描述符上的，用户感兴趣的IO事件

```
int s = socket(AF_INET, SOCK_STREAM, 0); 
bind(s, ...)
listen(s, ...)
int epfd = epoll_create(...);
epoll_ctl(epfd, ...); //将所有需要监听的socket添加到epfd中
while(1){
	int n = epoll_wait(...)
	for(接收到数据的socket){
		//处理
	}
}
```



### 基础网络编程

```
int s = socket(AF_INET, SOCK_STREAM, 0); //创建socket
bind(s, ...)//绑定
listen(s, ...)//监听
int c = accept(s, ...)//接受客户端连接
recv(c, ...);//接收客户端数据
```

### select

```
int s = socket(AF_INET, SOCK_STREAM, 0); 
bind(s, ...)
listen(s, ...)
int fds[] = 存放需要监听的socket
while(1){
	int n = select(..., fds, ...)
	for(int i=0; i < fds.count; i++){
		if(FD_ISSET(fds[i], ...)){
			//fds[i]的数据处理
		}
	}
}
```


