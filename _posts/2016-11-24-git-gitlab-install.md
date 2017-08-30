---
layout: post
title:  "Gitlab install"
date:   2016-12-16 12:00:00 +0900
categories: git gitlab
---


# GITLAB

## gitlab-ce 설치를 위한 패키지 설치및 방화벽 설정
```
yum install curl policycoreutils openssh-server openssh-clients
sudo systemctl enable sshd
sudo systemctl start sshd
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld
```

## gitlab-ce 설치
```
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
yum install gitlab-ce
gitlab-ctl reconfigure
```

## gitlab-ce 시작 종료 상태 명령어
```
gitlab-ctl start
gitlab-ctl stop
gitlab-ctl status
```
