# [Nmap参数详解（含扫描参数原理解释）](https://www.cnblogs.com/yurang/p/12046809.html)

- 语法结构：nmap [Scan Type(s)] [Options] {target specification}
- 端口状态介绍
  - open：确定端口开放，可达
  - closed ：关闭的端口对于nmap也是可访问的， 它接收nmap探测报文并作出响应。但没有应用程序在其上监听。
  - filtered ：由于包过滤阻止探测报文到达端口，Nmap无法确定该端口是否开放。过滤可能来自专业的防火墙设备，路由规则 或者主机上的软件防火墙。
  - unfiltered ：未被过滤状态意味着端口可访问，但是Nmap无法确定它是开放还是关闭。 只有用于映射防火墙规则集的 ACK 扫描才会把端口分类到这个状态。
  - open | filtered ：无法确定端口是开放还是被过滤， 开放的端口不响应就是一个例子。没有响应也可能意味着报文过滤器丢弃了探测报文或者它引发的任何反应。UDP，IP协议,FIN, Null 等扫描会引起。
  - closed|filtered：（关闭或者被过滤的）：无法确定端口是关闭的还是被过滤的
- 扫描目标格式
  - 示例： scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
  - -iL:从文件中加载目标
  - -iR:随机扫描
  - --exclude <host or network>:排除网段或主机地址
  - --excledefile:排除文件中的地址
- 主机发现
  - -sL:列出需要扫描的目标，不扫描
  - -sn:只做ping扫描，不做端口扫描
  - -Pn：跳过主机发现，视所有主机都在线
  - -PS/PA/PU/PY[portlist]：基于TCP（SYN、ACK）、UDP、SCTP的指定端口的主机发现
  - -PE/PP/PM：基于ICMP的echo、timestamp、network request的主机发现
  - -PO[Protocol list]：基于IP协议字段的ping扫描
  - -n/-R: -n表示不对目标最DNS解析，-R表示进行DNS解析，缺省为必要时候进行DNS解析
  - --dns-servers <serv1[,serv2],...>: 指定DNS 服务器
  - --system-dns:调用系统的DNS服务器
  - --traceroute：显示追踪到目标的路径
- 扫描技术
  - -sS/sT/sA/sW/sM:TCP扫描
    - S是SYN扫描，半连接扫描，nmap只发送SYN报文，通过服务器是否响应SYN+ACK来判断对应端口是否开放
    - T是全连接扫描会和服务器建立完整的三次握手，效率低
    - A发送ACK报文，通过服务器响应来判断是否开放，有的服务器不开会回复ICMP端口不可达，当回复RST时表示可能被拦截或者端口开放，不是一个准确的判断条件
    - W 是窗口扫描，发出的报文和ACK一样，利用的是在某些系统中如果端口开放，收到ACK包后会响应一个窗口非0的RST包
    - M是Maimon扫描，使用发现者的名字命名。其原理是向目标服务器发送FIN/ACK 报文，在某些系统中如果端口开放则会丢弃该报文不做响应，如果端口关闭则回复RST或者ICMP，Nmap可借此判断服务器端口的开放情况。不准
  - -sU：UDP扫描，某些系统如果UDP端口不开放会回复ICMP差错报文（这也是Linux系统中traceroute的实现原理）。Nmap UDP端口扫描的强大之处在于它会针对知名端口构造初始交互报文，比如会针对UDP 500构造一个主模式协商的IKE报文
  - -sN/sF/sX:特定TCP标志位的扫描，N是空标志位；F是FIN置位；X是Xmas扫描将FIN、PSH、URG同时置位。收到RST说明端口关闭，无响应说明被过滤或者端口开放，不准。
  - --scanflags <flags>：实现上同上面几种类似，可以让用户自定义TCP标志位。
  - -sI <zombie host[:probeport]>: Idle扫描需要一台没有流量的僵尸主机，这种扫描的实现原理是在一定的时间里，同一台主机发出的IP数据报文其ip头中的identification字段是累加的。探测分为3步：1、Nmap主机向僵尸机发包，通过僵尸机的响应包探测其ID；2、Nmap主机伪造僵尸机源地址向服务器的特定端口发送SYN包；3、Nmap主机再次探测僵尸机的ip.id。如果目标服务器端口开放，则必然会向僵尸机发送SYN/ACK，由于莫名其妙收到一个SYN/ACK 报文，僵尸机会向目标服务器发送RST报文，该报文的ip.id 是第一步+1，则第三步Nmap主机探测到的ip.id应该是第一步+2，说明目标主机端口开放。反之，如果目标主机端口未开放，则收到第二步的报文后会向僵尸机回复RST或者直接丢弃该报文不响应，无论哪种情况，都不会触发僵尸机发包，进而僵尸机的ip.id不会变化，第三步Nmap探测到的id应该是第一步+1.
  - -sY/sZ:SCTP协议INIT或cookie-echo扫描
  - -sO:基于IP协议的扫描，通过变换IP报文头中的Protocol值来对服务器进行探测
  - -b <FTP relay host>:：FTP反弹扫描，借助FTP特性，通过FTP服务器连接想要扫描的主机实现隐身的目的
- 端口相关参数
  - -p:指定端口扫描范围，如：-p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
  - --exclude-ports <port ranges>: 排除端口
  - -F：扫描比缺省少的端口（缺省1000，加了-F100）
  - -r：顺序扫描端口，缺省是随机分组扫描
  - --top-ports <number>:按top排序扫描知名端口
  - --port-ratio <ratio>: 按比例扫描知名端口，值在0-1之间，越小扫的越多
- 系统/版本探测
  - -sV:探测开放的端口的系统/服务信息
  - --version-intensity <level>:设置版本检测的详程度级别，0-9，越高越详细
  - --version-light：输出最可能的版本信息，缺省是2
  - --version-all：使用所有的探测条件进行版本/系统探测
  - --version-trace:打印详细的版本扫描过程
- 脚本扫描
  - --script=<Lua scripts>:指定脚本名称
  - --script-args=<n1=v1,[n2=v2,...]>:为脚本指定参数
  - --script-help=<Lua scripts>: 查看脚本帮助信息
  - --script-updatedb:更新脚本数据库
- 系统探测
  - -O:激活系统探测
  - --osscan-limit:只对开放端口的有效主机进行系统探测
  - --osscan-guess：推测系统信息
- 其他
  - -T<0-5>:时间模板，越大速度越快
  - -6：使能IPV6探测
  - -A：使能系统探测、版本检测、脚本扫描、路由追踪
  - -V：打印版本号
  - -v：增加输出的详细程度