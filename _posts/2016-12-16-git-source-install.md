---
layout: post
title:  "Git 소스 설치"
date:   2016-12-16 12:00:00 +0900
categories: git install
---

# GIT 소스설치

* 다운로드 ( https://www.kernel.org/pub/software/scm/git/ )
```
wget https://www.kernel.org/pub/software/scm/git/git-2.7.4.tar.gz

or

curl -o git-2.7.4.tar.gz https://www.kernel.org/pub/software/scm/git/git-2.7.4.tar.gz
```

* 압축풀기
```
tar -xvf git-2.7.4.tar.gz
```

* 설치
```
make prefix=/usr/local all

make prefix=/usr/local install
```