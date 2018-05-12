---
layout: post
title:  "centOS7 hostname 변경"
date:   2015-06-08 12:00:00 +0900
categories: ceontos 7
---

# CentOS 7.0 hostname 변경

CentOS 7 이전 버전에서는 /etc/sysconfig/network 파일에 HOSTNAME 을 정의하면 되었는데
CentOS 7 부터는 데비안 계열처럼 /etc/hostname 이라는 파일을 사용하도록 변경되었습니다.

/etc/sysconfig/network 파일은 보통 아래와 같이 설정을 합니다.

NETWORKING=yes
NETWORKING_IPV6=no
HOSTNAME=centos70
CentOS 7 에서는 이렇게만 하면 hostname 이 변경이 안 되고 hostnamectl 이라는 명령어를 사용하면 된다.

```bash
hostnamectl set-hostname centos7
```
hostname 을 확인해 볼려면 hostname 명령어를 실행해 보면 됩니다.

```bash
hostname
```

이렇게 hostname 을 설정을 하면 /etc/hostname 이라는 파일이 생성이 되어 있는 것을 확인할 수 있습니다. 우분투 등의 데비안 계열의 리눅스와 동일하게 변경되었습니다.

