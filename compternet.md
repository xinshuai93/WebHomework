# 计算机网络实验
## 验证性实验
+ **ipconfig**  
ipconfig 是微软操作系统的计算机上用来控制网络连接的一个命令行工具。它的主要用来显示当前网络连接的配置信息（/all 参数）。


    - 实作一、使用 ipconfig/all 查看自己计算机的网络配置，尽可能明白每行的意思，特别注意 IP 地址、子网掩码 Subnet Mask、网关 Gateway。
    ![image.png](https://s2.loli.net/2022/11/15/NOGg7FhMPCzIWnx.png)  
    可以看到我的ip地址为:192.168.43.245,子网掩码为:255.255.255.0,默认网关为:255.255.255.0
    - 实作二、使用 ipconfig/all 查看旁边计算机的网络配置，看看有什么异同。  
    下面为旁边计算机的网络配置，可以看出IP地址和MAC地址等不一样，网关地址一样和子网掩码一样。  
    问题 ：你的计算机和旁边的计算机是否处于同一子网，为什么？  
      IP地址的网络号相同，主机号不同，并且其子网掩码和网关相同；
    然后通过IP地址和子网掩码进行按位相与后得到相同的网络地址，所以其处于同一子网。
    （是处于同一子网，因为我们在同一个寝室通过网线连接到同个路由器上并接入校园网）


+ **Ping**  
PING （Packet Internet Groper），因特网包探索器，用于测试网络连接量的程序 。ping 是工作在 TCP/IP 网络体系结构中应用层的一个服务命令， 主要是向特定的目的主机发送 ICMP（Internet Control Message Protocol 因特网报文控制协议）Echo 请求报文，测试目的站是否可达及了解其有关状态。  
    - 实作一  
   要测试到某计算机如 重庆交通大学 Web 服务器的连通性，可以使用 ping www.cqjtu.edu.cn 命令，也可直接使用 IP 地址。
   请掌握使用该命令后屏幕显示的反馈回来信息的意思，如：TTL、时间等。  
   ![image.png](https://s2.loli.net/2022/11/15/MbN8reTUt2aJS5O.png)  
   可以看见能够ping通,对参数的说明如下：  
   字节=32：测试中发送的数据包大小是32个字节；  
   时间=40/169/48/149ms：与ping的目标对象主机往返一次所用的时间等于40/169/48/149ms,最短 = 40ms，最长 = 169ms，平均 = 101ms.  
   TTL=51：当前测试使用的TTL（Time to Live存活时间）值为51。  
   **ping自己的主机如下：**  
   ![image.png](https://s2.loli.net/2022/11/15/o9VHg4DBy6ka1rt.png)  
   - 实作二  
     使用 ping/? 命令了解该命令的各种选项并实际使用。  
     ![image.png](https://s2.loli.net/2022/11/15/p7TVjOM2enYKaAX.png)  
     实际应用如下：  
     1. 使用ping -t命令，指定ping继续向目标发送回显请求消息，直到中断（CTRL+C）  
     ![image.png](https://s2.loli.net/2022/11/15/HhgomGxZOlYvjqC.png)  
     2. 使用ping -a命令，指定在目标IP地址上执行的反向名称解析。  
     ![image.png](https://s2.loli.net/2022/11/15/KARFnu6wbj3UYJ1.png)  
     3. 使用ping -l size命令，指定回显请求消息中的数据字段的长度。  
     ![image.png](https://s2.loli.net/2022/11/15/uXjerbCQm73wESz.png)  
     **问题一**：假设你不能 ping 通某计算机或 IP，但你确定该计算机和你之间的网络是连通的，那么可能的原因是什么？该如何处理能保证 ping 通？  
     **答**：采用由近及远的连通性测试来确定问题所在。 比如我的计算机的IP地址为192.168.1.101，旁边计算机的IP地址为192.168.1.100，网关IP为192.168.1.1，那么：
     ping 127.0.0.1，测试自己计算机的状态，若成功，则说明本机网络软硬件工作正常，否则说明问题出现在本机，需检查本机TCP/IP配置即网卡状态等；ping 192.168.1.100，若成功，说明本子网内部工作正常，否则问题出现在本机网络出口到交换机之间，需检查本机网卡到交换机的连线等；ping 192.168.1.1，测试到网关的连通性，若成功，说明本子网出口工作正常，否则问题出现在网关，需报告给网管；ping 14.215.177.39，测试到百度的连通性，若成功则没有问题，否则问题出现在网关以外，自己无法解决。  
     **问题二**：假设ping 14.215.177.39没有问题，但ping百度的域名 www.baidu.com不行，那么可能的原因是什么？如何进行验证和解决？？  
     **答**：可能是DNS设置错误。由于计算机只识别IP地址，ping域名需要通过域名解析将域名转换成IP地址，而域名解析需要通过DNS进行，若DNS设置错误，可能导致域名解析不成功，进而无法ping通百度的域名。可通过清空DNS缓存或联系运营商解决。  
+ **tracert**  
TRACERT (Trace Route 的组合缩写)，也称为路由追踪，该命令行程序可用于跟踪 Internet 协议 （IP） 数据包传送到目标地址时经过的路径。  
    - 实作一  
     要了解到某计算机如 www.baidu.com 中间经过了哪些节点（路由器）及其它状态，可使用 tracert www.baidu.com 命令，查看反馈的信息，了解节点的个数。  
     ![image.png](https://s2.loli.net/2022/11/15/hJldOjsmkCuKIb4.png)  
     各个节点信息如下（依次展示）：  
     ![image.png](https://s2.loli.net/2022/11/15/RWJmSwMGLzgaKZp.png)  
     ![image.png](https://s2.loli.net/2022/11/15/vARN3SyQqf6VIt9.png)  
     ![image.png](https://s2.loli.net/2022/11/15/sKzTPFniouEv68w.png)  
     ![image.png](https://s2.loli.net/2022/11/15/RQdvwPBcL8h1SK9.png)  
     ![image.png](https://s2.loli.net/2022/11/15/7lCXn2kYf84s1jF.png)  
     ![image.png](https://s2.loli.net/2022/11/15/fv4yZYE95NcTlGb.png)  
     ![image.png](https://s2.loli.net/2022/11/15/Be9FoxUZ4aNLDXb.png)  
     ![image.png](https://s2.loli.net/2022/11/15/LNHnsIygWYjtazE.png)  
    - 实作二  
     ping.pe 这个网站可以探测从全球主要的 ISP 到某站点如 https://qige.io的线路状态，当然也包括各线路到该主机的路由情况。请使用浏览器访问 http://ping.pe/qige.io 进行了解。  
     ![image.png](https://s2.loli.net/2022/11/15/4e75SRHVME2IYLG.png)  
     ![image.png](https://s2.loli.net/2022/11/15/1YTfOxe9Hdk8MlN.png)  
     **问题一**：tracert能告诉我们路径上的节点以及大致的延迟等信息，那么它背后的原理是什么？  
     通过向目标地址发送不同IP存活时间值的“Internet控制消息协议（ICMP）”回应数据包，tracer诊断程序确定到目标地址所经过的路由。 要求路径上的每个路由器在转发数据包之前至少将数据包上的TTL递减1.数据包上的TTL减为0时，路由器应该将“ICMP已超时”的消息发回源系统。tracert先发送TTL为1的回应数据包，并在随后的每次发送过程将TTL递减1，直到目标响应或TTL达到最大值，从而确定路由。通过检查中间路由器发回的“ICMP已超时”的消息确定路由。某些路由器不经询问直接丢弃TTL过期的数据包，这在tracert使用程序中看不到。  
     **问题二**：在以上两个实作中，无论是访问百度还是棋歌教学网，路径中的第一条都是相同的，甚至似乎前几个节点都是相同的，你的解释是什么？  
     无论目的地址是什么，数据只要是从本机发送出去，都要到达同一个交换机，所以路径中的第一条都是相同的。前几个节点都相同可能是因为数据要出去需要经过网关，进而才能通过不同的子网到达不同的目的地址，而从本机过网关的路径都大致相同，所以前几个节点都是相同的。  
     **问题三**：在追踪过程中，你可能会看到路径中某些节点显示为 * 号，这是发生了什么？  
     该节点等待超时，没有出现具体的信息反馈。  
+ **ARP**
ARP（Address Resolution Protocol）即地址解析协议，是用于根据给定网络层地址即 IP 地址，查找并得到其对应的数据链路层地址即 MAC地址的协议。 ARP 协议定义在 1982 年的 RFC 826。  
    - **实作一**：  
    运行 arp -a 命令查看当前的 arp 缓存， 请留意缓存了些什么。  
    ![image.png](https://s2.loli.net/2022/11/15/wYJ5FeWqjAtd7zh.png)  
    **注意删除的时候需要执行管理员权限打开**  
    ![image.png](https://s2.loli.net/2022/11/15/Rfn1tG3iFpmzxD2.png)  
    ![image.png](https://s2.loli.net/2022/11/15/7hTG53tlDqmfLI8.png)  
    - **实作二**：  
      请使用 arp /? 命令了解该命令的各种选项。  
      ![image.png](https://s2.loli.net/2022/11/15/3bM7qWKzAyxfueC.png)
    - **实作三**：  
      一般而言，arp 缓存里常常会有网关的缓存，并且是动态类型的。  
      假设当前网关的 IP 地址是 192.168.43.245，MAC 地址是 5c-d9-98-f1-89-64，请使用 arp -s 192.168.0.1 5c-d9-98-f1-89-64 命令设置其为静态类型的。  
      ![image.png](https://s2.loli.net/2022/11/15/Qhq4rtLFU6moC8f.png)  
      出现此问题是因为win7及以上arp用来查mac，修改指定ip地址的时候需要使用netsh命令。  
      只要进入管理员模式，提高权限后再运行即可。  
      **问题一**:  
      在实作三中，为何缓存中常常有网关的信息？  
      **答**：因为缓存本身记录着你有访问过的pc 网卡MAC物理地址。  
      **问题二**：  
      我们将网关或其它计算机的 arp 信息设置为静态有什么优缺点？  
      **答**：优点是便于管理，特别是在根据IP地址限制网络流量的局域网中，以固定的IP地址或IP地址分组产生的流量为依据管理，可以免除在按用户方式计费时用户每次上网都必须进行的身份认证的繁琐过程，同时也避免了用户经常忘记密码的尴尬。静态分配IP地址的弱点是合法用户分配的地址可能被非法盗用，不仅对网络的正常使用造成影响
  
+ **DHCP**  
DHCP（Dynamic Host Configuration Protocol）即动态主机配置协议，是一个用于 IP 网络的网络协议，位于 OSI 模型的应用层，使用 UDP 协议工作，主要有两个用途：
  1. 用于内部网或网络服务供应商自动分配 IP 地址给用户.
  2. 用于内部网管理员对所有电脑作中央管理.  
简单的说，DHCP 可以让计算机自动获取/释放网络配置。
  - **实作一**：  
  一般地，我们自动获取的网络配置信息包括：IP 地址、子网掩码、网关 IP 以及 DNS 服务器 IP 等。使用ipconfig/release 命令释放自动获取的网络配置，并用 ipconfig/renew 命令重新获取，了解 DHCP 工作过程和原理。  
  ![image.png](https://s2.loli.net/2022/11/15/p7mYDEKebRkNw6T.png)  
  ![image.png](https://s2.loli.net/2022/11/15/kwhtO6mYzN3cE7H.png)  
  **问题一**：  
  在Windows系统下，如果由于某种原因计算机不能获取 DHCP 服务器的配置数据，那么Windows将会根据某种算法自动配置为 169.254.x.x 这样的 IP 地址。显然，这样的 IP 以及相关的配置信息是不能让我们真正接入 Internet 的，为什么？既然不能接入 Internet，那么Winodws系统采用这样的方案有什么意义？  
  因为自动配置的IP地址和信息只是短暂性的解决计算机不能获取 DHCP 服务器的配置数据的问题，要真正的接入Internet还是得本身计算机的正确IP地址。意义是假如某天因DHCP服务器问题从而不能获得网络配置，那么我们可以查看隔壁教室计算机的配置信息来手动进行网络配置，从而使该计算机能够接入Internet。
+ **netstat**  
无论是使用 TCP 还是 UDP，任何一个网络服务都与特定的端口（Port Number）关联在一起。因此，每个端口都对应于某个通信协议/服务。
netstat（Network Statistics）是在内核中访问网络连接状态及其相关信息的命令行程序，可以显示路由表、实际的网络连接和网络接口设备的状态信息，以及与 IP、TCP、UDP 和 ICMP 协议相关的统计数据，一般用于检验本机各端口的网络服务运行状况。
  - **实作一**:  
  Windows 系统将一些常用的端口与服务记录在 C:\WINDOWS\system32\drivers\etc\services文件中，请查看该文件了解常用的端口号分配。  
  ![image.png](https://s2.loli.net/2022/11/15/dWBSnsoxFY5X8f4.png)  
  - **实作二**:  
  使用 netstat -an 命令，查看计算机当前的网络连接状况。更多的 netstat 命令选项.  
  ![image.png](https://s2.loli.net/2022/11/15/hGZk6yOCrE15N8I.png)  
  ![image.png](https://s2.loli.net/2022/11/15/1XFrEftSzDcG3L2.png)  
+ **NDS**  
DNS（Domain Name System）即域名系统，是互联网的一项服务。它作为将域名和 IP 地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。DNS 使用 TCP 和 UDP 的 53 号端口。  
  - **实作一**：  
  Windows 系统将一些固定的/静态的 DNS信息记录C:\WINDOWS\system32\drivers\etc\hosts 文件中，如我们常用的 localhost 就对应127.0.0.1 。请查看该文件看看有什么记录在该文件中。  
  ![image.png](https://s2.loli.net/2022/11/15/7ytLQ8vSOg5JxAB.png)  
  - **实作二**：  
  解析过的 DNS 记录将会被缓存，以利于加快解析速度。请使用 ipconfig /displaydns 命令查看。我们也可以使用ipconfig /flushdns 命令来清除所有的 DNS 缓存。  
  ![image.png](https://s2.loli.net/2022/11/15/WAcjn1UDaRbg68P.png)  
  删除缓存：  
  ![image.png](https://s2.loli.net/2022/11/15/km8n7PHI9yDSZFG.png)  
  - **实作三**：  
  - 使用 nslookup qige.io 命令，将使用默认的 DNS 服务器查询该域名。当然你也可以指定使用
  CloudFlare（1.1.1.1）或 Google（8.8.8.8） 的全球 DNS 服务器来解析，如：nslookup qige.io
  8.8.8.8，当然，由于你懂的原因，这不一定会得到正确的答案。  
  ![image.png](https://s2.loli.net/2022/11/15/z7gpmZYLtojbsyI.png)  
  **问题一**：使用插件或自己修改hosts文件来屏蔽广告，思考一下这种方式为何能过滤广告？如果某些广告拦截失效，那么是什么原因？你应该怎么进行分析从而能够成功屏蔽它？  
  hosts文件是一个用于存储计算机网络中节点信息的文件，它可以将主机名映射到相应的IP地址，实现DNS的功能，它可以由计算机的用户进行控制。  
  hosts相当于一个字典，如果查到输入的域名在hosts之中，则会先调用其对应的IP，而不通过DNS，因此能够通过手动添加修改错误的<ip-网址>来达到屏蔽某网站的目的。通过将127.0.0.1广告链接设置为广告推送链接，从而广告链接就不会访问到本机，而是访问它自己的服务器。  
+ **catch**  
cache 即缓存，是 IT 领域一个重要的技术。我们此处提到的 cache 主要是浏览器缓存。
浏览器缓存是根据 HTTP 报文的缓存标识进行的，是性能优化中简单高效的一种优化方式了。一个优秀的缓存策略可以缩短网页请求资源的距离，减少延迟，并且由于缓存文件可以重复利用，还可以减少带宽，降低网络负荷。
  - **实作一**  
  打开 Chrome 或 Firefox 浏览器，访问 https://qige.io ，接下来敲 F12 键 或 Ctrl +Shift + I 组合键打开开发者工具，选择 Network 面板后刷新页面，你会在开发者工具底部看到加载该页面花费的时间。请进一步查看哪些文件被 cache了，哪些没有。  
  经过对比可以发现一些图片，js文件和txt文件被缓存了，而一些CSS文件没有  
  ![image.png](https://s2.loli.net/2022/11/15/tjdhnOoiDJB5I9C.png)  
  - **实作二**  
  接下来仍在 Network 面板，选择 Disable cache 选项框，表明当前不使用 cache，页面数据全部来自于Internet，刷新页面，再次在开发者工具底部查看加载该页面花费的时间。你可比对与cache 时的加载速度差异。  
  ![image.png](https://s2.loli.net/2022/11/15/EHtZdLDqnfcAs7e.png)  
+ **验证性实验心得体会**  
通过使用cmder在命令行窗口中实现前面七个常规的命令操作，让我对计算机网络有了初步的认识和理解，了解到了各个命令的作用。最后在浏览器中打开开发者工具后取消cache选项，经过前后的网页呈现速度对比也让我对cache缓存的作用有了进一步的认识。  


## WireShark实验
+ **数据链路层**  
+ **实作一**：熟悉 Ethernet 帧结构 使用 Wireshark 任意进行抓包，熟悉 Ethernet 帧的结构，如：目的 MAC、源 MAC、类型、字段等。  
![image.png](https://s2.loli.net/2022/11/15/R6HLVrJ2QKi1weN.png)  
  - **问题一**：你会发现 Wireshark 展现给我们的帧中没有校验字段，请了解一下原因。  
  Wireshark 抓包前，在物理层网卡已经去掉了一些之前几层加的东西，比如前导同步码，FCS等等，之后利用校验码CRC校验，正确时才会进行下一步操作，因此，抓包软件抓到的是去掉前导同步码、FCS之外的数据，没有校验字段。   
+ **实作二**：了解子网内/外通信时的 MAC 地址  
  - ping 你旁边的计算机（同一子网），同时用 Wireshark 抓这些包（可使用 icmp
关键字进行过滤以利于分析），记录一下发出帧的目的 MAC 地址以及返回帧的源 MAC 地址是多少？这个 MAC 地址是谁的？
ping同一子网内的ip：192.168.88.18  
![image.png](https://s2.loli.net/2022/11/17/xOFGb1jczQyHDvJ.png)  
![image.png](https://s2.loli.net/2022/11/17/4YrhFT3JwyQf6Iq.png)




