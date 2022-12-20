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
  - 然后 ping qige.io （或者本子网外的主机都可以），同时用 Wireshark 抓这些包（可 icmp 过滤），记录一下发出帧的目的 MAC 地址以及返回帧的源 MAC 地址  
  ![image.png](https://s2.loli.net/2022/12/19/Z9hR5STQXd7vNyP.png)
  ![image.png](https://s2.loli.net/2022/12/19/WxlIKNCVrH3LpjD.png)
  - 再次 ping www.cqjtu.edu.cn （或者本子网外的主机都可以），同时用 Wireshark 抓这些包（可 icmp 过滤），记录一下发出帧的目的 MAC 地址以及返回帧的源 MAC 地址又是多少？这个 MAC 地址又是谁的？
  - ![image.png](https://s2.loli.net/2022/12/19/Szvbyg4JTHrZmGw.png)
  - ![image.png](https://s2.loli.net/2022/12/19/OS4Gor6bjZVgxRN.png)
  通过以上的实验，你会发现：  
  访问本子网的计算机时，目的 MAC 就是该主机的,访问非本子网的计算机时，目的 MAC 是网关的
  请问原因是什么？  
  **答**：不出入子网不需要经过网关，所以MAC是主机的；网关是出入本子网和其他子网需要到达的地方，所以目的MAC是网关的。  
+ **实作三**: 掌握 ARP 解析过程  
  1. 为防止干扰，先使用 arp -d * 命令清空 arp 缓存  
  2. ping 你旁边的计算机（同一子网），同时用 Wireshark 抓这些包（可 arp 过滤），查看 ARP 请求的格式以及请求的内容，注意观察该请求的目的 MAC 地址是什么。再查看一下该请求的回应，注意观察该回应的源 MAC 和目的 MAC 地址是什么。  
  3. 再次使用 arp -d * 命令清空 arp 缓存  
  4. 然后 ping qige.io （或者本子网外的主机都可以），同时用 Wireshark 抓这些包（可 arp 过滤）。查看这次 ARP 请求的是什么，注意观察该请求是谁在回应。  
    ![image.png](https://s2.loli.net/2022/12/19/Hhb13gOGUfsWroL.png)
    可以看到ping同一子网时，使用arp过滤后，请求的目的MAC地址为全F，说明为广播。
    ![image.png](https://s2.loli.net/2022/12/19/3KqBPWJMkbNYxrT.png)
    而ping qige.io时，回复的就是网关。
    - **问题**:通过以上的实验，你应该会发现，ARP 请求都是使用广播方式发送的，如果访问的是本子网的 IP，那么 ARP 解析将直接得到该 IP 对应的 MAC；如果访问的非本子网的 IP， 那么 ARP 解析将得到网关的 MAC。  
      请问为什么？  
      **答**：因为ARP代理，访问非子网IP时是通过路由器访问的，路由器再把发出去，目标IP收到请求后，再通过路由器端口IP返回回去，那么ARP解析将会得到网关的MAC。  
### 网络层
+  **实作一：熟悉 IP 包结构**  
    - 使用 Wireshark 任意进行抓包（可用 ip 过滤），熟悉 IP 包的结构，如：版本、头部长度、总长度、TTL、协议类型等字段。  
    ![image.png](https://s2.loli.net/2022/12/19/bX5dq7sWZMCjg68.png)
    通过ip过滤后，可知该ip版本号为ipv4  
    头部长度为20bytes  
    总长度为386  
    TTL为2  
    - **问题**：为提高效率，我们应该让 IP 的头部尽可能的精简。但在如此珍贵的 IP 头部你会发现既有头部长度字段，也有总长度字段。请问为什么？  
    **答**：便于传输时的识别IP总长度，因为接收端需要读数据，接收数据当长度超过1500B时就会被返回链路层进行分段，有标明可以有效节省时间。  
+  **实作二：IP包的分段与重组**
    - 根据规定，一个 IP 包最大可以有 64K 字节。但由于 Ethernet 帧的限制，当 IP 包的数据超过 1500 字节时就会被发送方的数据链路层分段，然后在接收方的网络层重组。缺省的，ping 命令只会向对方发送 32 个字节的数据。我们可以使用 ping 202.202.240.16 -l 2000 命令指定要发送的数据长度。此时使用 Wireshark 抓包（用 ip.addr == 202.202.240.16 进行过滤），了解 IP 包如何进行分段，如：分段标志、偏移量以及每个包的大小等。
    ![image.png](https://s2.loli.net/2022/12/19/4T6CxfSBnHepQ5r.png)  
    ![image.png](https://s2.loli.net/2022/12/19/RvmsdGFgDJcSf46.png)
    - **问题**：
    分段与重组是一个耗费资源的操作，特别是当分段由传送路径上的节点即路由器来完成的时候，所以 IPv6 已经不允许分段了。那么 IPv6 中，如果路由器遇到了一个大数据包该怎么办？  
    **答**：应该要丢弃掉，并且不要忘记通知对方已经丢弃掉了。
+ **实作三：考察 TTL 事件**
    - 在 IP 包头中有一个 TTL 字段用来限定该包可以在 Internet上传输多少跳（hops），一般该值设置为 64、128等。在验证性实验部分我们使用了 tracert 命令进行路由追踪。其原理是主动设置 IP 包的 TTL 值，从 1 开始逐渐增加，直至到达最终目的主机。请使用 tracert www.baidu.com 命令进行追踪，此时使用 Wireshark 抓包（用 icmp 过滤），分析每个发送包的 TTL 是如何进行改变的，从而理解路由追踪原理。  
    - ![image.png](https://s2.loli.net/2022/12/19/PGFz6VpItBHTvMk.png)  
    - ![image.png](https://s2.loli.net/2022/12/19/Pg3WOnE4ljtkSL8.png)  
    - 这里可以看到抓到的包中的TTL是不断增加的。
    - **问题**：
    在 IPv4 中，TTL 虽然定义为生命期即 Time To Live，但现实中我们都以跳数/节点数进行设置。如果你收到一个包，其 TTL 的值为 50，那么可以推断这个包从源点到你之间有多少跳？  
    如果是64跳得话，就是64-50 = 14跳，而128跳得话就是78。
### 传输层
+ **实作一：熟悉 TCP 和 UDP 段结构**  
  1. 用 Wireshark 任意抓包（可用 tcp 过滤），熟悉 TCP 段的结构，如：源端口、目的端口、序列号、确认号、各种标志位等字段。  
     用wireshark抓包后用tcp过滤得到。
     ![image.png](https://s2.loli.net/2022/12/19/X3k9mYTQegBiqJI.png)
  2. 用 Wireshark 任意抓包（可用 udp 过滤），熟悉 UDP 段的结构，如：源端口、目的端口、长度等。  
  3. ![image.png](https://s2.loli.net/2022/12/19/zTX2WM3RUDve6ug.png)
  **问题**：  
  由上大家可以看到 UDP 的头部比 TCP 简单得多，但两者都有源和目的端口号。请问源和目的端口号用来干什么？  
  **答**：用来找应用程序。
+ **实作二: 分析 TCP 建立和释放连接**
  1. 打开浏览器访问 qige.io 网站，用 Wireshark 抓包（可用 http 过滤后再使用加上 Follow TCP Stream），不要立即停止 Wireshark 捕获，待页面显示完毕后再多等一段时间使得能够捕获释放连接的包。  
   ![image.png](https://s2.loli.net/2022/12/19/7eIWG5sp9oHr31M.png)
  2. 请在你捕获的包中找到三次握手建立连接的包，并说明为何它们是用于建立连接的，有什么特征。  
   - 第一次握手：SYN = 1;ACK = 0;
   ![image.png](https://s2.loli.net/2022/12/19/nyfb2Js7jme3FiS.png)
   - 第二次握手：SYN = 1;ACK = 1;
   - ![image.png](https://s2.loli.net/2022/12/19/PamScp9jKlxs1TI.png)
   - 第三次握手：SYN = 0;ACK = 1;
   - ![image.png](https://s2.loli.net/2022/12/19/5YVOEfbMANyDvds.png)
   - **在TCP协议中，通信双方将通过三次TCP报文实现对以上信息的了解，并在此基础上建立一个TCP连接，通信双方的三次TCP报文段的交换过程为建立连接的过程。**
  **问题一**:  
  去掉 Follow TCP Stream，即不跟踪一个 TCP 流，你可能会看到访问 qige.io 时我们建立的连接有多个。请思考为什么会有多个连接？作用是什么？  
  **答**：因为这个连接属于短连接，这为了实现多个用户进行访问，对业务频率不高的场合，不让其长期占用通道。  
  **问题二**:  
  我们上面提到了释放连接需要四次挥手，有时你可能会抓到只有三次挥手。原因是什么？  
  **答**：如果被动方迅速调用close函数，那么被动方的ACK和FIN有可能在一个报文中发送。这样就可能只抓到三次挥手。
### 应用层
+ **实作一: 了解 DNS 解析**:  
  1. 先使用 ipconfig /flushdns 命令清除缓存，再使用 nslookup qige.io 命令进行解析，同时用 Wireshark 任意抓包（可用 dns 过滤）。  
  2. ![image.png](https://s2.loli.net/2022/12/19/Os6re5TpiPdxmL3.png)
  ![image.png](https://s2.loli.net/2022/12/19/K8GtLfnyOXWUbFN.png)
  1. 你应该可以看到当前计算机使用 UDP，向默认的 DNS 服务器的 53 号端口发出了查询请求，而 DNS 服务器的 53 号端口返回了结果。  
  2. ![image.png](https://s2.loli.net/2022/12/19/BmytXRzoUcLYxp6.png)
  3. 可了解一下 DNS 查询和应答的相关字段的含义  
   DNS应答字段含义:  
  1.QR：查询/应答标志。0表示这是一个查询报文，1表示这是一个应答报文  
  2.opcode，定义查询和应答的类型。0表示标准查询，1表示反向查询（由IP地址获得主机域名），2表示请求服务器状态  
  3.AA，授权应答标志，仅由应答报文使用。1表示域名服务器是授权服务器  
  4.TC，截断标志，仅当DNS报文使用UDP服务时使用。因为UDP数据报有长度限制，所以过长的DNS报文将被截断。1表示DNS报文超过512字节，并被截断  
  5.RD，递归查询标志。1表示执行递归查询，即如果目标DNS服务器无法解析某个主机名，则它将向其他DNS服务器继续查询，如此递归，直到获得结果并把该结果返回给客户端。0表示执行迭代查询，即如果目标DNS服务器无法解析某个主机名，则它将自己知道的其他DNS服务器的IP地址返回给客户端，以供客户端参考  
  6.RA，允许递归标志。仅由应答报文使用，1表示DNS服务器支持递归查询  
  7.zero，这3位未用，必须设置为0  
  8.rcode，4位返回码，表示应答的状态。常用值有0（无错误）和3（域名不存在）清除缓存  
  **问题**:  
  你可能会发现对同一个站点，我们发出的 DNS 解析请求不止一个，思考一下是什么原因？  
  DNS不止一个的原因可能是DNS解析过程是先从浏览器的DNS缓存中检查是否有这个网址的映射关系，如果有，就返回IP，完成域名解析；等等一系列过程，直到获得对应的IP为止。
+ **实作二: 了解 HTTP 的请求和应答**:  
  1. 打开浏览器访问 qige.io 网站，用 Wireshark 抓包（可用http 过滤再加上 Follow TCP Stream），不要立即停止 Wireshark 捕获，待页面显示完毕后再多等一段时间以将释放连接的包捕获。  
   ![image.png](https://s2.loli.net/2022/12/19/AcUmX9MFNlBegOI.png)
  2. 请在你捕获的包中找到 HTTP 请求包，查看请求使用的什么命令，如：GET, POST。并仔细了解请求的头部有哪些字段及其意义。  
   ![image.png](https://s2.loli.net/2022/12/19/nYLvbDh5IKlPHOk.png)
  3. 请在你捕获的包中找到 HTTP 应答包，查看应答的代码是什么，如：200, 304, 404 等。并仔细了解应答的头部有哪些字段及其意义。  
    状态码：  
    1xx：接收到请求且正在处理  
    2xx：请求正常处理完毕：eg：200 OK  
    3xx：重定向状态，表示浏览器需要进行附加操作  
    4xx：服务器无法处理这个请求 eg ：404 Page Not Found  
    5xx：服务器处理出错 eg：502 Bad Gateway  

    **建议**：HTTP 请求和应答的头部字段值得大家认真的学习，因为基于 Web 的编程中我们将会大量使用。如：将用户认证的令牌信息放到头部，或者把 cookie 放到头部等。  
    **问题**:  
    刷新一次 qige.io 网站的页面同时进行抓包，你会发现不少的 304 代码的应答，这是所请求的对象没有更改的意思，让浏览器使用本地缓存的内容即可。那么服务器为什么会回答 304 应答而不是常见的 200 应答？  
    **答**：  
    200（成功） 服务器已成功处理了请求。通常，这表示服务器提供了请求的网页。如果是对您的 robots.txt 文件显示此状态码，则表示 Googlebot 已成功检索到该文件。  
    304（未修改）  
    自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容。如果网页自请求者上次请求后再也没有更改过，您应将服务器配置为返回此响应（称为 If-Modified-Since HTTP 标头）。服务器可以告Googlebot 自从上次抓取后网页没有变更，进而节省带宽和开销


## Cisco Packet Tracer 实验
+ **请大家先了解 VLSM、CIDR、RIP、OSPF、VLAN、STP、NAT 及 DHCP 等概念，以能够进行网络规划和配置。**
  1. **VLSM**(可变长子网掩码) 是为了有效的使用无类别域间路由（CIDR）和路由汇聚(route summary)来控制路由表的大小，它是网络管理员常用的IP寻址技术，VLSM就是其中的常用方式，可以对子网进行层次化编址，以便最有效的利用现有的地址空间。
  2. **CIDR**一般指无类别域间路由。 无类别域间路由（Classless Inter-Domain Routing、CIDR）是一个用于给用户分配IP地址以及在互联网上有效地路由IP数据包的对IP地址进行归类的方法。
  3. **RIP**(Routing Information Protocol,路由信息协议）是使用最久的协议之一。RIP是一种分布式的基于距离向量的路由选择协议。
  4. **OSPF**一般指组播扩展OSPF。 OSPF(Open Shortest Path First开放式最短路径优先）是一个内部网关协议(Interior Gateway Protocol，简称IGP），用于在单一自治系统（autonomous system,AS）内决策路由。
  5. **VLAN**一般指虚拟局域网。 VLAN（Virtual Local Area Network）的中文名为"虚拟局域网"。虚拟局域网（VLAN）是一组逻辑上的设备和用户，这些设备和用户并不受物理位置的限制。
  6. **STP**（Spanning Tree Protocol）是生成树协议的英文缩写，可应用于计算机网络中树形拓扑结构建立，主要作用是防止网桥网络中的冗余链路形成环路工作。
  7. **NAT**（Network Address Translation），是指网络地址转换，1994年提出的。当在专用网内部的一些主机本来已经分配到了本地IP地址（即仅在本专用网内使用的专用地址），但又想和因特网上的主机通信（并不需要加密）时，可使用NAT方法。
  8. **DHCP**（动态主机配置协议）是一个局域网的网络协议。指的是由服务器控制一段IP地址范围，客户机登录服务器时就可以自动获得服务器分配的IP地址和子网掩码。
+ **直接连接两台 PC 构建 LAN**  
  将两台 PC 直接连接构成一个网络。注意：直接连接需使用交叉线.进行两台 PC 的基本网络配置，只需要配置 IP 地址即可，然后相互 ping 通即成功。  
  ![image.png](https://s2.loli.net/2022/12/20/L751QfgIClu2pNA.png)
  ![image.png](https://s2.loli.net/2022/12/20/yFnOHGmlq3ue8KI.png)
  ![image.png](https://s2.loli.net/2022/12/20/rO2vF5RYj47NUgo.png)
  ![image.png](https://s2.loli.net/2022/12/20/eWFzpnB86dOUV1D.png)
+ **用交换机构建 LAN**:  
构建如下拓扑结构的局域网：  
   1.  PC0 能否 ping 通 PC1、PC2、PC3 ？
    ![image.png](https://s2.loli.net/2022/12/20/zSoCrxiJuBHInNW.png)
    ![image.png](https://s2.loli.net/2022/12/20/djCQYMGnFRTvDaS.png)
    ![image.png](https://s2.loli.net/2022/12/20/POy2KYFGNpJI7A1.png)
    ![image.png](https://s2.loli.net/2022/12/20/JlQTGifo5KIShdU.png)
   2. PC3 能否 ping 通 PC0、PC1、PC2 ？为什么？
    ![image.png](https://s2.loli.net/2022/12/20/tOixK2VuZg7Bhmq.png)
    **答**：同一个子网内部的主机互相可以通信，不在同一子网不能通信。
   3. 将 4 台 PC 的掩码都改为 255.255.0.0 ，它们相互能 ping 通吗？为什么？  
     ![image.png](https://s2.loli.net/2022/12/20/lmvj6wBX5YGrtRS.png)  
     ![image.png](https://s2.loli.net/2022/12/20/sTdOrEKp8x4vgYB.png)  
     可以ping通的原因是此时四台主机，都处于192.168.0.0这一子网下。
   4. 使用二层交换机连接的网络需要配置网关吗？为什么？  
     **答**：需要配置网关。二层交换机的网关主要用于远程登录（SSH/telnet）管理，以及发生故障的时候，可以通过SNMP trap消息向网管系统发送报警消息。
+ **交换机接口地址列表**：  
  1. 仍然构建上图的拓扑结构，并配置各计算机的 IP 在同一个一个子网，使用工具栏中的放大镜点击某交换机如左边的 Switch3，选择 MAC Table，可以看到最初交换机的 MAC 表是空的，也即它不知道该怎样转发帧（那么它将如何处理？），用 PC0 访问（ping）PC1 后，再查看该交换机的 MAC 表，现在有相应的记录，请思考如何得来。随着网络通信的增加，各交换机都将生成自己完整的 MAC 表，此时交换机的交换速度就是最快的！  
   ![image.png](https://s2.loli.net/2022/12/20/wc1EfMUFSGegYR5.png)
   ![image.png](https://s2.loli.net/2022/12/20/varNWSf9TebEAV2.png)
   ![image.png](https://s2.loli.net/2022/12/20/ZKOegHkdhfcUTxC.png)
+ **生成树协议（Spanning Tree Protocol）**：
   1. 交换机在目的地址未知或接收到广播帧时是要进行广播的。如果交换机之间存在回路/环路，那么就会产生广播循环风暴，从而严重影响网络性能。而交换机中运行的 STP 协议能避免交换机之间发生广播循环风暴。只使用交换机，构建如下拓扑：  
    ![image.png](https://s2.loli.net/2022/12/20/Ush45gqMfZTzLYv.png)
    这是初始时的状态。我们可以看到交换机之间有回路，这会造成广播帧循环传送即形成广播风暴，严重影响网络性能。
    随后，交换机将自动通过生成树协议（STP）对多余的线路进行自动阻塞（Blocking），以形成一棵以 Switch5 为根（具体哪个是根交换机有相关的策略）的具有唯一路径树即生成树！
    经过一段时间，随着 STP 协议成功构建了生成树后，Switch4 的两个接口当前物理上是连接的，但逻辑上是不通的，处于Blocking状态（桔色）如下图所示：  
    ![image.png](https://s2.loli.net/2022/12/20/oGLibw7fRxj5p1J.png)  
    在网络运行期间，假设某个时候 Switch5与 Switch4 之间的物理连接出现问题（将 Switch5 与 Switch4 的连线剪掉），则该生成树将自动发生变化。上方那个接口仍处于 Blocking 状态（桔色）。如下图所示：  
    ![image.png](https://s2.loli.net/2022/12/20/vAao4tVxXDH6lGM.png)