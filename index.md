{% include "../include/header.md" %}

# Docker 설명서

- 출처 및 참고 : [pyrasis](http://pyrasis.com/Docker/Docker-HOWTO)

## Docker Install

##### yum으로 docker설치

```bash
[root@7cent ~]# yum install docker
Loaded plugins: fastestmirror, langpacks

~~ blahblah ~~

Installed:
  docker.x86_64 0:1.6.0-11.0.1.el7.centos

Dependency Installed:
  audit-libs-python.x86_64 0:2.4.1-5.el7
  checkpolicy.x86_64 0:2.1.12-6.el7
  docker-selinux.x86_64 0:1.6.0-11.0.1.el7.centos
  libcgroup.x86_64 0:0.41-8.el7
  libsemanage-python.x86_64 0:2.1.10-16.el7
  policycoreutils-python.x86_64 0:2.2.5-15.el7
  python-IPy.noarch 0:0.75-6.el7
  setools-libs.x86_64 0:3.3.7-46.el7

Complete!
```
간편하게 도커 패키지 실행


##### 설치 확인
```bash
[root@7cent ~]# docker --version
Docker version 1.6.0, build 8aae715/1.6.0
```
**1.6버전 빌드** 확인

##### 도커 이미지 확인
```bash
[root@7cent ~]# docker images
FATA[0001] Get http:///var/run/docker.sock/v1.18/images/json: dial unix /var/run/docker.sock: no such file or directory. Are you trying to connect to a TLS-enabled daemon without TLS?
```
도커 이미지를 확인하려했으나 에러발생

##### 도커 데몬 실행
```bash
[root@7cent ~]# systemctl start docker.service
[root@7cent ~]# chkconfig docker on
알림: 'systemctl enable docker.service'에 요청을 전송하고 있습니다.
ln -s '/usr/lib/systemd/system/docker.service' '/etc/systemd/system/multi-user.target.wants/docker.service'
[root@7cent ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
```
도커를 부팅시에 올라오게 설정하고 데몬을 실행, 그리고 현재 이미지가 아무것도 없음을 확인


## Install Ubuntu

##### CeontOS7 위에 Docker로 Ubuntu 설치
```bash
[root@7cent ~]# docker pull ubuntu:latest
latest: Pulling from docker.io/ubuntu

e118faab2e16: Pull complete
7e2c5c55ef2c: Pull complete
e04c66a223c4: Pull complete
fa81ed084842: Already exists
docker.io/ubuntu:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.

Digest: sha256:738edd684282277c07f23277718e43562daf2ee210f7aca9a13fae65f0159ddd
Status: Downloaded newer image for docker.io/ubuntu:latest
[root@7cent ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
docker.io/ubuntu    latest              fa81ed084842        3 days ago          188.3 MB
```
Docker에서 Ubuntu 최신 버전을 받고 현재 받은 이미지 확인 latest(최신버전) 을 받았습니다.

##### Docker 실행
```bash
docker run -i -t --name test ubuntu /bin/bash
```
-i ( interactive), -t(Pseudo-tty) 옵션을 사용해서 Bash Shell에 입력 및 출력을 할 수 있습니다.
--name 옵션은 test란 이름의 container를 생성합니다.
도커를 실행합니다.

##### Docker Container 목록 확인
```bash
[root@7cent ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
48faba53180c        ubuntu:latest       "/bin/bash"         13 minutes ago      Exited (0) 12 minutes ago                       test
```
docker ps 하면 현재 실행중인 Container만 보입니다. -a 옵션을 통해 모든 도커 컨테이너를 확인합니다.
현재 test도커가 있음을 확인할 수 있습니다.

##### test(Ubuntu) Container 실행 및 접속
```bash
[root@7cent ~]# docker start test
test
[root@7cent ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
48faba53180c        ubuntu:latest       "/bin/bash"         15 minutes ago      Up 2 seconds                            test
[root@7cent ~]# docker attach test
root@48faba53180c:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@48faba53180c:/#
```
test Container 를 실행하고 ps 명령어로 올라와있는지 확인합니다.
이후 attach 명령어로 해당 Container 쉘에 접근합니다.
보통 ** Ctrl+D ** 혹은 ** exit ** 로 쉘을 종료하게 되는데 이러면 Docker Container가 종료됩니다.
** Ctrl+P ** 를 누른후 ** Ctrl+Q ** 를 연속으로 누르면 Container가 살아있는 채로 HostOS로 빠져 나올 수 있습니다.

##### Docker Container 확인, 종료, 삭제
```bash
[root@7cent ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
48faba53180c        ubuntu:latest       "/bin/bash"         30 minutes ago      Up 5 minutes                            test
[root@7cent ~]# docker stop test
test
[root@7cent ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
48faba53180c        ubuntu:latest       "/bin/bash"         30 minutes ago      Exited (0) 7 seconds ago                       test
[root@7cent ~]# docker rm test
test
[root@7cent ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
나와서 확인해보면 test Container가 실행중임을 확인 할 수 있습니다.
해당 Container를 멈추면 Status가 Exited상태로 변함을 알 수 있습니다.
docker rm test 명령어를 통해 Container를 삭제 하였습니다.
docker ps -a 명령어를 통해 Container가 완전 삭제 되었음을 확인 할 수 있습니다.

##### Docker Image 삭제
```bash
[root@7cent ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
docker.io/ubuntu    latest              fa81ed084842        3 days ago          188.3 MB
[root@7cent ~]# docker rmi ubuntu:latest
Untagged: ubuntu:latest
Deleted: fa81ed084842076d1b39b56d084d99ec0011cd4a5ade1056be359486a8b213e4
Deleted: e04c66a223c45a6247237510c40117cef92acb0a4355f1ba90580ef6274b490d
Deleted: 7e2c5c55ef2cd7675dcc9e9cc012dc2f759ceaf0f36c950b672af6df87af5070
Deleted: e118faab2e16f9d858fcec0d86c9148e9b0fa021697239745f3253f367941dcc
[root@7cent ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
```
docker images 를 확인하면 pull받았던 ubuntu 이미지가 존재함을 확인 할 수있는데
docker rmi ubuntu:latest 명령어를 통해 해당 이미지를 삭제 할 수 있습니다.
다시한번 확인해보면 해당 이미지가 삭제 되었음을 확인 할 수 있습니다.


{% include "../include/footer.md" %}