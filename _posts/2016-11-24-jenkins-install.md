# JENKINS

## jenkins 레파지터리 등록 및 설치
```
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum install jenkin
```

## 포트 변경 및 방화벽 등록
vim /etc/sysconfig/jenkins
> JENKINS_PORT="9000"

```
firewall-cmd --zone=public --add-port=9000/tcp --permanent
firewall-cmd --reload
```

## jenkins 시작 종료 상태 명령어
```
systemctl start jenkins.service
systemctl stop jenkins.service
systemctl status jenkins.service
```


## jenkins 사용자 및 권한 관리
> Jenkins관리 - Configure Global Security  
- Enable security 체크
- Jenkins' own user database 체크 (사용자 가입 허용 안함)
- Authorization 항목에서 Matrix-based security (유저별 권한 설정)

## jenkins 권한 관리 잘못 저장하면
```
vim /var/lib/jenkins/config.xml 
```
> useSecurity 항목을 false 처리하고 jenkins 재시작
