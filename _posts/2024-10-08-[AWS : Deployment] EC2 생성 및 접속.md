---
title : "[AWS] EC2 생성 및 접속"
date : 2024-10-08 12:12:00 +0900
categories : [AWS, Deployment]
tags : [aws] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

# [AWS] EC2 생성 및 접속

### 들어가기에 앞서
 교내 팀 프로젝트를 통해 백엔드 개발 다수 존재하지만, 환경 구축이나 배포 경험은 부족하다. 이번 학기에는 "다우기술"의 사내 문제를 해결하는 해커톤 형태의 과목을 수강하게 되었고, 팀원들과 역할을 분담하여 초기 백엔드 환경 구축 및 배포를 맡게 되었다.

해당 글은 기록용으로 부족한 부분이 있을 수 있습니다. 참고 부탁드립니다.

## AWS란?
---
AWS(Amazon Web Services)는 클라우드 컴퓨팅을 통해 다양한 서비스를 제공하는 플랫폼으로, 전 세계적으로 사용되는 안전하고 확장 가능한 인프라를 제공한다. 이를 통해 사용자는 서버 자원을 유연하게 조정하고 관리할 수 있으며, 초기 비용 없이 필요한 만큼만 비용을 지불할 수 있다.

본 글에서는 EC2를 사용하여 진행할 것이다.

### EC2 인스턴스 생성 및 설정
인스턴스 생성은 다른 블로그에서 많이 다루고 있는 내용이니 생략하겠다.

보안 규칙은 다음과 같이 설정해둔다
<img width="1170" alt="image 2" src="https://github.com/user-attachments/assets/80d6e825-dce5-400c-a47a-9ef298c899b7">

### EC2 Instance Console에 접속
인스턴스 생성 시 발급 받은 pem 키가 있을 것이다. 

```bash
chmod 400 이름.pem
```

해당 명령어로 권한을 변경하여 준다.

~~~bash
ssh -i /경로/이름.pem ec2-user@인스턴스-퍼블릭-ip
~~~

<img width="874" alt="스크린샷 2024-10-07 13 44 06" src="https://github.com/user-attachments/assets/c42a98a3-e11e-4320-ab85-165b32fbbe3a">

