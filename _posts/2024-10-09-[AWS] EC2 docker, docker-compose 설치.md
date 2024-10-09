---
title : "[AWS] EC2 docker, docker-compose 설치"
date : 2024-10-09 20:03:00 +0900
categories : [AWS, Deployment]
tags : [aws] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

# [AWS] EC2 docker, docker-compose 설치

다음으로 SpringBoot 배포를 위해 docker와 docker-compose를 설치할 것이다.

## 1. Docker란?
----
Docker는 애플리케이션을 실행할 수 있는 가벼운 가상화 환경인 컨테이너를 생성하는 도구이다. 컨테이너는 시스템의 전체 운영체제를 복제하는 대신, 필요한 부분만 분리하여 애플리케이션을 격리된 환경에서 실행할 수 있게 한다. 이를 통해 개발 환경과 배포 환경의 일관성을 유지하고, 리소스를 효율적으로 사용할 수 있다.

Docker는 개별 컨테이너를 만들고 실행하는 데 사용되며, 주로 하나의 애플리케이션 또는 서비스를 컨테이너화할 때 활용된다. 반면에 **Docker Compose**는 여러 컨테이너를 정의하고 관리할 수 있는 도구로, 복잡한 애플리케이션에서 여러 서비스(예: 웹 서버, 데이터베이스 등)를 한 번에 설정하고 실행할 수 있도록 도와준다. **Docker Compose**를 사용하면 docker-compose.yml 파일에서 설정을 정의하고, 한 명령어로 여러 컨테이너를 일괄적으로 관리할 수 있다.

## 2. Docker 설치 방법
---
### 1.  yum update
```bash
sudo yum update -y
```

### 2. install docker
```bash
sudo yum install docker -y
```

### 3. service docker
```bash
sudo service docker start
```

### 4. grant permission to ec2-user
```bash
sudo usermod -a -G docker ec2-user
```

### 5. Docker service start and enable automatic startup
```bash
sudo systemctl start docker
sudo systemctl enable docker
```


## 3. Docker-compose 설치 방법
yum에는 기본적으로 Docker Compose 패키지가 없기 때문에, 직접 바이너리를 다운로드하여 설치해야 한다.
### 1. Docker-compose 바이너리 파일 다운로드
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### 2. 실행 권한 부여
```bash
sudo chmod +x /usr/local/bin/docker-compose
```

### 3. 설치 확인
```bash
docker-compose --version
```

🚨 Error loading Python lib '/tmp/_MEILqk4h0/libpython3.7m.so.1.0' 에러 발생 시🚨
~~~bash
sudo yum install libxcrypt-compat
~~~


<img width="874" alt="image" src="https://github.com/user-attachments/assets/ab75bd32-1db5-475d-a535-d69817944395">