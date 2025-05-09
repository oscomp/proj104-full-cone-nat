# proj104-full-cone-nat
为nftables实现Full-cone NAT


# 项目描述



网络地址转换（Network Address Translation, abbr. NAT）在计算机网络中是一种在IP数据包通过路由器或防火墙时重写来源IP地址（Source NAT, abbr. SNAT）或目的IP地址（Destination NAT，abbr. DNAT）的技术。这种技术被普遍使用在有多台主机但只通过一个公有IP地址访问互联网的私有网络中。RFC 3489规定了4类NAT类型：Full Cone、Restricted Cone、Port Restricted Cone、Symmetric。

NAT会话穿越应用程序（Session Traversal Utilities for NAT，abbr. STUN）是一种网络协议，它允许位于NAT（或多重NAT）后的客户端找出自己的公网地址，查出自己位于那种类型的NAT之后以及NAT为某一个本地端口所绑定的Internet端端口。这些信息被用来在两个同时处于NAT路由器之后的主机之间创建UDP通信，它被广泛应用于VoIP、WebRTC、网络游戏等设计低延迟的点到点通讯领域。该协议由RFC 5389定义。基于STUN的内网穿透成功率取决于通信双方的NAT类型，其中 Full Cone NAT 的成功率最高。

Linux内核树上未实现真正意义上的Full Cone NAT，Linux的 SNAT/MASQUERADE均是symmetric NAT。

Linux Kernel只实现了Symmetric NAT，有人曾为iptables实现了full-cone NAT。但当前各大Linux发行版正从iptables迁往nftables，iptables所使用的内核模块（前缀为xt）逐渐地被nftables内核模块（前缀为nf）替代。因此可以为nftables实现相应的full cone NAT模块。

- NAT: https://en.wikipedia.org/wiki/Network_address_translation
- RFC 3489: https://datatracker.ietf.org/doc/html/rfc3489
- STUN: https://en.wikipedia.org/wiki/STUN
- RFC 5389: https://datatracker.ietf.org/doc/html/rfc5389
- 从DNAT到netfilter内核子系统，浅谈Linux的Full Cone NAT实现: https://blog.chionlab.moe/2018/02/09/full-cone-nat-with-linux/
  - https://github.com/Chion82/netfilter-full-cone-nat

# 所属赛道

2025全国大学生操作系统比赛的“OS功能设计”赛道

# 参赛要求

- 请遵循“2025全国大学生操作系统比赛”的章程和技术方案要求

### 项目导师

付林

- blog: https://vvl.me

- email: fulin10@huawei.com river@vvl.me

### 难度

中等

# 特性

为nftables实现full cone NAT，可以通过STUN full cone NAT测试。

实现包括两部分：

- 基于Linux kernel nftables框架的内核模块
- 基于iptables-nft的用户态控制程序，或基于nftables的用户态控制程序

参考资料：

- Adding new expressions to nftables：https://zasdfgbnm.github.io/2017/09/07/Extending-nftables/
- nftables wiki：https://wiki.nftables.org/wiki-nftables/index.php/Main_Page

# 进阶特性

1. 实现Restricted Cone NAT
2. 实现Port Restricted Cone NAT

# License

GPL

# 预期目标

1. 基本的环境的搭建与熟悉
   - 搭建STUN服务器，测试所处IPv4网络环境的NAT类型
   - 编译并运行项目https://github.com/Chion82/netfilter-full-cone-nat代码，确认使用后的NAT类型为full cone
2. 编写基于Linux kernel nftables框架的内核模块，能够通过STUN full cone NAT类型测试
3. 编写基于iptables-nft的用户态控制程序，或基于nftables的用户态控制程序
4. 实现Restricted Cone NAT
5. 实现Port Restricted Cone NAT
