# Tcpdump basics

1、参数组成格式

`tcpdump [options] [proto] [direction] [net type]`

options: 可选参数

proto: 协议类过滤器 tcp or udp or icmp or arp ......

direction: 数据流向过滤器 src or dst

type: 网络类型过滤器 host or net or port or portrange......

`tcpdump host 172.29.231.26`

`tcpdump -i enp1s0 arp src 172.29.231.26`

`tcpdump src net 192.168.10.0/24`

`tcpdump src port 80 or 8088`

`tcpdump src portrange 8000-8080`

`tcpdump tcp port http`

`tcpdump 'ip proto tcp'`

`tcpdump ip proto 6`

`tcpdump 'ip6 proto tcp'`

`tcpdump 'src 10.0.2.4 and (dst port 3389 or 22)'`



2、输出内容格式

时间 + 网络协议 + 源主机及端口 + 数据流向符号 + 目标主机及端口 + 冒号 + 报文内容

`10:18:16.255803 IP TCGLFVHNBGW02.ssh > 192.168.157.38.63961: Flags [P.], seq 4208533652:4208533860, ack 543395016, win 3111, length 208`

`10:20:27.490501 ARP, Request who-has 172.29.231.25 tell 172.29.231.26, length 46`



3、常用可选参数

\-n: IP 显示

\-nn: 不转化协议和端口号

\-N: 不打印 host 域名部分

\-w: 输出到文件中

\-r: 从文件中读取

\-v: 控制输出内容详细程度，-vv -vvv

\-t: 控制时间显示程度, -tt -ttt -tttt

\-x: 显示数据包头部, -xx -X -XX

\-i: 指定网卡接口

\-Q: 过滤方向 in, out, inout，也可以使用 --direction=\[direction]

\-A: 以 ASCII 码方式显示每一个数据包

\-l: 行输出，便于保存和解析

\-q: 简洁打印和输出

\-c: 捕获指定数量数据包

\-s: tcpdump 默认只会截取前 96 字节的内容，要想截取所有的报文内容，可以使用 -s number， number 就是你要截取的报文字节数，如果是 0 的话，表示截取报文全部内容

\-S: 使用绝对序列号，而不是相对序列号

\-C: file-size，tcpdump 在把原始数据包直接保存到文件中之前, 检查此文件大小是否超过file-size. 如果超过了, 将关闭此文件,另创一个文件继续用于原始数据包的记录. 新创建的文件名与-w 选项指定的文件名一致, 但文件名后多了一个数字.该数字会从1开始随着新创建文件的增多而增加. file-size的单位是百万字节

\-F: 使用file 文件作为过滤条件表达式的输入, 此时命令行上的输入将被忽略

\-D: 显示所有可用网络接口的列表

\-e: 每行的打印输出中将包括数据包的数据链路层头部信息

\-d: 打印出易读的包匹配码 -dd -ddd

\-Z: 后接用户名，在抓包时会受到权限的限制。如果以root用户启动tcpdump，tcpdump将会有超级用户权限

\-E: 解密 IPSEC 数据

\-L: 列出指定网络接口所支持的数据链路层的类型后退出



4、常用过滤关键字

if：表示网卡接口名

proc：表示进程名&#x20;

pid：表示进程 id&#x20;

svc：表示 service class&#x20;

dir：表示方向，in 和 out&#x20;

eproc：表示 effective process name&#x20;

epid：表示 effective process ID



5、特殊过滤规则

1）根据 tcpflags 进行过滤

tcpdump 支持我们根据数据包的标志位进行过滤，tcp\[tcpflags] 等价于 tcp\[13]

tcp-fin, tcp-syn, tcp-rst, tcp-push, tcp-ack, tcp-urg 别名常量，分别代表 1，2，4，8，16，32，64

proto \[ expr:size ]

proto：可以是熟知的协议之一（如ip，arp，tcp，udp，icmp，ipv6）

expr：可以是数值，也可以是一个表达式，表示与指定的协议头开始处的字节偏移量。

size：是可选的，表示从字节偏移量开始取的字节数量。

`tcpdump -i eth0 "tcp[13] & tcp-syn != 0"`

`tcpdump -i eth0 'tcp[tcpflags] == tcp-syn or tcp[tcpflags] == tcp-ack'`

tcp 中有 类似 tcp-syn 的别名常量，其他协议也是有的



2）基于包大小进行过滤

`$ tcpdump less 32`&#x20;

`$ tcpdump greater 64`&#x20;

`$ tcpdump <= 128`



3）根据 mac 地址进行过滤

`$ tcpdump ether host [ehost]`&#x20;

`$ tcpdump ether dst [ehost]`&#x20;

`$ tcpdump ether src [ehost]`



4）过滤通过指定网关的数据包

`tcpdump gateway [host]`



5）过滤广播/多播数据包

`$ tcpdump ether broadcast $ tcpdump ether multicast`

`$ tcpdump ip broadcast $ tcpdump ip multicast`

`$ tcpdump ip6 multicast`



只抓取 HTTP 的 GET 请求示例

`tcpdump -s 0 -A -vv 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420'`

`tcpdump -vvAls0 | grep 'GET'`

`tcp[n:c]：`表示 tcp 报文里从第n个字节开始取 c 个字节，tcp\[12:1] 表示从报文的第12个字节（因为有第0个字节，所以这里的12其实表示的是13）开始算起取一个字节，也就是 8 个bit。这里只需要报文首部中的偏移量。

&：是位运算里的 and 操作符，比如 0011 & 0010 = 0010

\>>: 是位运算里的右移操作

0xf0：是 10 进制的 240 的 16 进制表示

实际数据开始的位置: (tcp\[12:1] & 0xf0) >> 2，其实就是 偏移量 乘以偏移单位的简化写法。(tcp\[12:1] & 0xf0) >> 4 ) << 2 偏移单位为 四字节。

从数据开始的位置再取出四个字节，然后将结果与 GET （注意 GET最后还有个空格）的 16进制写法（也就是 0x47455420）进行比对

`0x47455420 GET 的 ASCII 码十六进制写法`

`0x47 --> 71 --> G 0x45 --> 69 --> E 0x54 --> 84 --> T 0x20 --> 32 --> 空格`

找出发包数最多的 IP

`tcpdump -nnn -t -c 200 | cut -f 1,2,3,4 -d '.' | sort | uniq -c | sort -nr | head -n 20`

切割 pcap 文件

tcpdump -w /tmp/capture-%H.pcap -G 3600 -C 200

提取 HTTP POST 请求中的密码

`tcpdump -s 0 -v -n -l | egrep -i "POST /|GET /|Host:"`

提取 HTTP 请求的 URL

`tcpdump -s 0 -v -n -l | egrep -i "POST /|GET /|Host:"`

抓取 HTTP 有效数据包

`tcpdump 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)'`

利用管道将抓包文件重定向到 wireshark 中解析

`ssh root@remotesystem 'tcpdump -s0 -c 1000 -nn -w - port 53' | /Applications/Wireshark.app/Contents/MacOS/Wireshark -k -i -`
