---
title : "[AWS] SpringBoot, MariaDB 연결하기"
date : 2024-10-15 11:21:00 +0900
categories : [AWS, Deployment]
tags : [aws] #소문자만 가능
toc: true
toc_sticky: true
published : true
---
# [AWS] SpringBoot, MariaDB 연결하기


## 1. 패키지 설치
### 1. 설치 가능한 mariadb 패키지 검색
```bash
sudo yum search mariadb
```
### 2. Mariadb 설치
```bash
sudo yum install mariadb105-server.x86_64 -y 
```
### 3. Mariadb 실행
```bash
sudo systemctl start mariadb
```
### 4. Mariadb root 비밀번호 설정
```bash
sudo mysql_secure_installation
```
### 5. 로그인 확인
```bash
sudo mysql -u root -p
```


## 2. 그외 설정
### 1. Docker 이미지 다운로드
```bash
docker pull mariadb
```
### 2. DB 생성 및 사용자 설정
```bash
sudo mysql -u root -p
```

```sql
create user 'tester'@'%' identified by 't1234';
grant all privileges on *.* to 'tester'@'%';
flush privileges;
```

## 3. SpringBoot 프로젝트 설정
#### 1. build.gradle 의존성 추가
```gradle
dependencies {
    implementation 'org.mariadb.jdbc:mariadb-java-client:3.1.0'
}
```
### 2. application.yml, application-local.yml 파일 생성
#### 1. src/main/resources/application.yml
```yml
server:
  address: 0.0.0.0
  port: 8080

spring:
  application:
    name: springboot_ex
  profiles:
    active: local
```

#### 2. src/main/resources/application-local.yml
```yml
spring:
  datasource:
    url: jdbc:mariadb://localhost:3306/test
    username: tester
    password: t1234
    driver-class-name: org.mariadb.jdbc.Driver

  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        format_sql: true
        show_sql: true
      dialect: org.hibernate.dialect.MariaDBDialect
```

### 2. docker-compose.yml 수정
```yml
version: '3.1'
services:
  mariadb:
    container_name: mariadb_container
    image: mariadb:latest
    restart: always
    ports:
      - "3306:3306"
    volumes:
      - "./mariadb/conf.d:/etc/mysql/conf.d"
      - "./mariadb/data:/var/lib/mysql"
    environment:
      MARIADB_DATABASE: test
      MARIADB_USER: tester
      MARIADB_PASSWORD: t1234
      MARIADB_ROOT_PASSWORD: "1234"

  application:
    container_name: backend_container
    build:
      context: ./
      dockerfile: Dockerfile
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mariadb://mariadb:3306/test
      SPRING_DATASOURCE_USERNAME: "tester"
      SPRING_DATASOURCE_PASSWORD: "t1234"
    depends_on:
      - mariadb
    volumes:
      - ./src/main/resources/application.yml:/app/config/application.yml
    command: [ "java", "-jar", "app.jar", "--spring.config.location=file:/app/config/application.yml" ]
```
![](2024-10-08-%5BAWS%20:%20Deployment%5DSpringBoot,%20MariaDB%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5/image%202.png)
## 🔥 dbeaver 접속 성공