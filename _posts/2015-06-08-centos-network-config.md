---
layout: post
title:  "centOS7 network 변경"
date:   2015-06-08 12:00:00 +0900
categories: ceontos 7
---

# CentOS 7 에서 네트워크 설정

##### CentOS 7에서 네트워크 인터페이스의 명칭이 변경되었습니다.

지금까지는 "eth ~" 였는데,
7.0부터는 "en ~ ' 로 바뀌었다. (예. enp0s2)
설정 파일의 위치는 : "/etc/sysconfig/network-script" 아래에 있습니다.

```bash
[root@7cent ~] $ ls -la /etc/sysconfig/network-scripts/ifcfg*
-rw-r - r-- 1 root root 321 8 월 8 09:03 /etc/sysconfig/network-scripts/ifcfg-enp0s2
-rw-r - r-- 1 root root 254 8 월 3 09:30 /etc/sysconfig/network-scripts/ifcfg-lo
```
네트워크를 설정해 보겠습니다.

기본은 dhcp로 되어있습니다.
```bash

HWADDR="00:00:29:08:A5:37"
TYPE="Ethernet"
BOOTPROTO="dhcp"
DEFROUTE="yes"
PEERDNS="yes"
PEERROUTES="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_PEERDNS="yes"
IPV6_PEERROUTES="yes"
IPV6_FAILURE_FATAL="no"
NAME="enp0s3"
UUID="b3d0246c-d2ba-49c7-98fb-2c394b30e29b"
ONBOOT="yes"
```

고정 IP로 바꿔보겠습니다.
고정 IP "10.10.91.244"로 바꿔보겠습니다.

```bash
HWADDR="00:00:29:08:A5:37"
TYPE="Ethernet"
BOOTPROTO="none"
DEFROUTE="yes"
PEERDNS="yes"
PEERROUTES="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_PEERDNS="yes"
IPV6_PEERROUTES="yes"
IPV6_FAILURE_FATAL="no"
NAME="enp0s3"
UUID="b3d0246c-d2ba-49c7-98fb-2c394b30e29b"
ONBOOT="yes"

# IP Address
IPADDR = "10.10.91.244"
# Subnet Mask
NETMASK = "255.255.254.0"
# Default Gateway
GATEWAY = "10.10.90.1"
# DNS Server
DNS1 = "168.126.63.1"
```
바뀐 부분은 세번째 줄에 "BOOTPROTO"의 값을 "dhcp"에서 "none"으로 변경하고,
(IP 주소, 서브넷 마스크, 기본 게이트웨이, DNS 서버)의 내용을 추가하면 된다.
설정 파일을 수정했다면 네트워크를 다시 시작합니다.

systemctl restart NetworkManager
systemctl restart network

Cent OS 7.0의 네트워크 설정이 완료되었습니다.

[출처 : 만석이의 예술 이야기](http://manseok.blogspot.kr/2014/08/centos-70.html)

