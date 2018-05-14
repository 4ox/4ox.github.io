---
layout: post
title:  "centos6 setting"
date:   2016-03-24 22:25:36 +0900
categories: centos
---


# centos7 설정값

- 초기 설정
```
// PC 비프음 제거
rmmod -v pcspkr

// hostname 변경
vim /etc/hostname
>> env

// network on
vi /etc/sysconfig/network-script/ifcfg-{blahblah}
>> 변경
onboot=YES

> 재부팅 혹은 네트워크 재시작
init 6 
systemctl network restart

// upgrade
yum upgrade -y

// vim 설치
yum install -y vim

// ifconfig 보기위한 툴 설치
yum install net-tools

// iptalbes 설치 및 등록
yum install -y iptables-services
systemctl enable iptables

```

- 환경 설정
```
// JDK 설치
> 설치 가능 목록 확인 및 1.8버전 설치
yum list java*jdk-devel
yum install -y java-1.8.0-openjdk-devel.x86_64

> 설치 확인
java -version
javac -version

// TOMCAT7 설치 
> 기본 페키지에 없는 레파지토리 설치
yum install -y yum-plugin-priorities

> jpackage 레파지토리 추가 ( java 패키지 )
wget -O- http://www.jpackage.org/jpackage.asc | gpg --import

> tomcat7 설치 목록 확인
yum list tomcat7* | grep tomcat

> tomcat7 설치
 yum install -y tomcat7 tomcat7-admin-webapps tomcat7-webapps --skip-broken

> 방화벽 열기
iptables -I INPUT 1 -p tcp --dport 8080 -j ACCEPT


// 시간 동기화

> ntp & libedit & ntpdate 설치
yum -y install ntp
 
> peer 설정
vi /etc/ntp.conf
>> 수정
server time.bora.net
server time.kornet.net

> 시작프로그램에 등록
systemctl enable ntpd.service
 
> 서비스 시작
systemctl start ntpd.service
 
> 확인
ntpq -p



> rdate 설치
yum -y install rdate
 
> 하드웨어 시간확인
hwclock -r
> 시간설정
hwclock -w (운영체제값과 동기화)
hwclock -s (운영체제 값을 동기화 시킴)
 
> 운영체제 시간확인
date
 
> 타임서버 시간확인
rdate -p time.bora.net
> 시간설정
rdate -s time.bora.net
 
> 시스템 부팅시 동기화
vi /etc/rc.d/rc.local
>> 추가
/usr/bin/rdate -s time.bora.net
/sbin/hwclock -w

> cron을 이용한 주기적인 동기화
crontab -e
>> 매일새벽 1시동기화 추가
00    01    *    *    *    /usr/bin/rdate -s time.bora.net&&hwclock -w


// TOMCAT7 설치

yum install tomcat7
>> Package tomcat7-7.0.54-2.jpp6.noarch.rpm is not signed  ( 이런 오류가 나면 )
vim /etc/yum.repos.d/jpackage.repo
>> gpgcheck=0


```
