---
title : "[AWS] Docker로 SpringBoot 배포하기"
date : 2024-10-20 18:30:00 +0900
categories : [AWS, Deployment]
tags : [aws] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

# [AWS] Docker로 SpringBoot 배포하기

앞서 EC2 리눅스 콘솔 환경에 docker와 docker-compose를 설치하였다. 다음은 이를 사용하여 서버에 SpringBoot를 배포하는 작업을 수행할 것이다. 


### Dockerfile
* **Dockerfile**은 컨테이너 이미지를 빌드하기 위한 스크립트
* 애플리케이션이 실행되는 환경을 정의하며, 필요한 라이브러리 설치, 애플리케이션 소스 코드 복사, 실행 명령어 등을 포함

> **Dockerfile**은 애플리케이션의 "설치 가이드"와 같으며, 이를 기반으로 docker build 명령어를 통해 이미지를 생성

### docker-compose.yml
* **docker-compose.yml** 파일은 여러 Docker 컨테이너를 정의하고, 이들 간의 관계를 설정하는 데 사용
* 복잡한 애플리케이션에서는 여러 개의 컨테이너가 필요함(예: 웹 서버, 데이터베이스 서버, 캐시 서버 등). 이때 **docker-compose.yml**을 사용하여 각 컨테이너의 설정을 한 번에 정의하고 관리할 수 있음

> docker-compose up 명령어로 정의된 모든 컨테이너를 한 번에 실행 가능


## 1. Dockerfile, docker-compose.yml 작성

두 파일이 프로젝트 루트 폴더에 존재하도록 생성합니다.

### Dockerfile
```dockerfile
FROM openjdk:17
WORKDIR /app
COPY build/libs/springboot_ex-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
ENV TZ=Asia/Seoul
```

### docker-compose.yml
```yml
version: '3'
services:
  springboot-app:
    build: .
    ports:
      - "8080:8080"
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```

## 2. 컨테이너 실행시키기

### 1. 프로젝트 빌드
~~~bash
./gradle build
~~~

### 2. 이미지 생성
```bash
docker build -t springboot_ex .
```

### 3. 컨테이너 실행
```bash
docker-compose up -d
```

### 4. 상태 확인
```bash
docker container ls -al
```

<img width="1357" alt="image" src="https://github.com/user-attachments/assets/c9e3ec3e-ef96-483b-b9bf-f8ec02459dd2">

<img width="884" alt="image 2" src="https://github.com/user-attachments/assets/d771bb81-57ec-4eae-bb86-8f926df5ee56">


컨테이너가 성공적으로 실행됐고, 접속도 잘 되고 있다.

## 3. 서버에 필요한 패키지 설치 
먼저 앞서 만든 프로젝트를 Github Repository를 생성하여 올려준다.

### 1. 서버에 git 설치
```bash
sudo yum install git -y
```

### 2. 설치 가능한 패키지 리스트 확인 
```bash
yum list java*
```

### 3. JDK 설치
```bash
sudo yum install java-17-amazon-corretto-devel
```
*Dockerfile의 jdk 버전과 동일하게*

### 4. 설치 확인
```bash
java --version
```

## 4. 배포

```bash
git clone https://github.com/레포지토리 주소

cd 레포지토리 이름

./gradle build

docker build -t springboot_ex .

docker-compose up -d

docker container ls -al
```

**🚨 docker: permission denied while trying to connect to the Docker daemon socket at 오류**
> sudo chmod 666 /var/run/docker.sock

<img width="1240" alt="image 3" src="https://github.com/user-attachments/assets/8485a5f1-eca1-4439-8f4d-bfbd58825075">

## 정상적으로 접속되는 것을 볼 수 있다.