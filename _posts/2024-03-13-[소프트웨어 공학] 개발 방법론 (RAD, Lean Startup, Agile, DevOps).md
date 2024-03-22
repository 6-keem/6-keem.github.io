---
title : "[소프트웨어 공학] 소프트웨어 개발 방법론 개발 방법론 (RAD, Lean Startup, Agile, DevOps)"
date : 2024-03-13 10:23:00 +0900
categories : [소프트웨어 공학, 정리]
tags : [software engineering] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

## 소프트웨어 개발 방법론

---

### 1. RAD (Rapid Application Development)

> 사용자의 지속적 참여하에서 빠르게 애플리케이션을 개발하기 위한 개발 라이플 사이클 모델

* 빠른 애플리케이션 개발을 위한 자동 생성 도구
* 지속적인 참여 및 피드백을 통한 개선

#### 1.1 RAD의 특성

* 고객 참여 - 피드백
* 신속 개발 - **Risk ↓** 분야에 사용
* 짧은 주기 - 개발기간이 짧음

RAD vs Waterfall 비교

|             MODEL              |       RAD       |  Waterfall  |
| :----------------------------: | :-------------: | :---------: |
|        **Wating time**         |      short      |    long     |
|            **Risk**            |       low       |    high     |
|           **Budget**           |    not fixed    |    fixed    |
|     **Approach of Change**     |     anytime     | Not welcome |
|      **Quality Control**       |   throughout    | at the end  |
| **High technical application** | Not appropriate | appropriate |
|      **Not for end user**      |       No        |     Yes     |



----



### 2. Lean Startup (지속적)

고객이 원하지 않는 제품을 만드는 것이 스타트업의 가장 큰 위험이라는 모토를 가짐

#### 2.1 Lean Startup의 특성

* 아이디어를 빠르게 제품화 시키고 피드백을 반영하여 지속적 제품 개선

* 고객의 피드백을 받아 시장의 니즈를 파악하는 전략

*※ Startup : 불확실성을 환경에서 신규 서비스나 제품 개발하는 조직*

#### 2.2 Lean Startup Process

```아이디어 (가설 설정)``` -> ```만들기 (MVP를 통한 가설 검증)``` ->``` 제품``` -> ```측정``` -> ```데이터``` -> ```학습```

**<ins>MVP (Minimum Viable Product)</ins>**

> 아이디어의 빠른 제품화를 통해 고객의 피드백을 바탕으로 발전시킴

#### 2.3 지속적 프로세스

* 가설 설정, 학습이 일회성이 아닌 지속적

* 학습한 내용을 바탕으로 완전 새로운 제품으로 방향전환<ins>**(pivot)**</ins> 가능

  *※ 반드시 동작할 필요는 없음 (DropBox)*



---



### 3. Agile Process (반복, 점진적)

> **반복적이고 점진적인** 개발 방법 <ins>**(IID, Iterative and Incremental Development)**</ins>에 기반

점진적 개발 : 이전 시스템에 피드백을 반영하여 추가적 개발

**반복적 개발 : 한 번에 개발하는 것이 아닌 반복적으로 개선하고 수정**

※ 두 개발의 구분 필요

#### 3.1 반복적 점진적 개발과 불확실성

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/06976d89-95ea-4745-9f1e-5f8dce865017" alt="애자일" style="zoom:50%;" />

* 개발 초기 모든 **불확실성 제거 불가능**
* 고객의 **피드백을 바탕으로 다음 제품에 반영**하는 것이 좋음
* 제품을 개발하며 제품을 만드는 좋은 방법을 학습함

#### 3.2 Agile vs Waterfall

Watefall - **전통적/순차적인 개발 모델**으로 **문제가 잘 정의** 되어있고 **예측이 가능**하며 **큰 변화가 없는 시스템 개발**에 사용

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/d7ca2ddf-65a5-4fff-a363-3308e9fa6c41" alt="애자일과폭포수" style="zoom:50%;" />

| Model                | Agile              | Waterfall        |
| -------------------- | ------------------ | ---------------- |
| 가치(작동 제품) 전달 | 각 Iteration       | 최종 단계        |
| 리스크               | 가치 전달할 수록 ↓ | 시간 지날 수록 ↑ |
| 피드백 수용 여부     | O                  | X                |

#### 3.3 IID (Iterative and Incremental Development)

* 소프트웨어 개발 주기를 여러 Iteration주기로 개발 (각 **Iteration**은 Waterfall 프로젝트)
* 각 **주기 요구분석, 설계 구현, 테스트**를 가짐
* 각 반복주기가 종료되면 동작하는 제품이 나옴
* 고객에게 전달되는 것은 최종 반복주기 산출물

* 각 주기(1~4주)마다 새로운 요구사항 추가됨
* **가장 높은 가치전달**이 가능한 요구사항을 **우선 순위를 높게** 두고 **각 반복주기 시작전에 선택**하여 개발
* 고객의 **피드백 환영**하지만 Iteration **시작되면 요구사항 변경 X**

#### 3.4 Agile Team - (팀 단위 보상 필요)

​	**1. self-organizing** - 외부 명령, 통제 없이 스프린트 목적 달성을 위한 최상의 방법 선택 

​	**2. cross-functional** - 다른 팀원의 역할도 대신 수행할 수 있음

※ 3주차 Scrum 정리에서 자세히 다룸

#### 3.5 Agile Manifest (영어 표현 추가하기)

* 공정과 도구 < **개인과 상호작용**

* 포괄적인 문서 < **작동하는 소프트웨어**

* 계약 협상 < **고객과 협력**

* 계획을 따르기 < **변화에 대응 (Emergent)**

  *※ Agile : 민첩한, 날렵한*

<ins>**Todo**</ins> : PPT의 적응성, 대응성, 효율성, 혁신, 소유권 내용 공부



#### 3.6 Agile Principles 

https://agilemanifesto.org/iso/ko/principles.html



---



### 4. DevOps (<ins>Dev</ins>elopment <ins>**Op**</ins>eration<ins>**s**</ins>)

> **개발팀과 운용팀과 긴밀한 협업**으로 비즈니스 요구에 **신속한 대응**
>
> 배포된 소프트웨어가 운영 환경에서 **안정적으로 동작**하도록 하여 비즈니스 가치 실현

#### 4.1 개발팀 vs 운영팀의 대립

* 개발 : 비즈니스 요구에 맞춰 새로운 기능 요구에 **신속한 대응**

* 운용 : 변화보다는 **안정성**에 관심

``` 개발과 운용 모두 공통의 목적 의식을 갖고 서로 존중하며 협력 필요 ```

*※ 공통 목적 : 요구사항 신속 대응 및 안정적 서비스 제공*

#### 4.2 DevOps 프로세스 (Infinite loop)

![DevOps](https://github.com/6-keem/BlogImageRepository/assets/113224939/4983da5f-f254-40da-b90f-24bfce8a07d6)

* Plan : 요구사항 정의
* Code : 구현 코드를 저장소에 Commit
* Build : 문제가 없는지 검사 후 통합
* Test : 배포할 준비가 되었는지 테스트
* Release : 최종 산출물 관리 
* Deploy : 배포
* Operate/Monitor : 운영 환경 데이터 수집, 분석, 결과 통지 및 피드백



#### 4.3 Waterfall vs Agile vs DevOps

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/f0c49d5d-6ff3-40da-9623-ed003dee662c" alt="방법론비교" style="zoom:50%;" />



#### 4.4 CI와 CD

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/91486359-b47c-4651-a914-13be1dd2415c" alt="CICD" style="zoom:50%;" />

> CI (Continuous Intergration) - 지속적 통합
>
> CD (Continuous Delivery) - 지속적 전달

* Big Bang Intergration : Intergration Hell

  *※ 코드가 종료시점에 한 번에 통합*

  * 뒤늦은 결함 발견
  * 오류 파악 어려움
  * 배포 불가능
  * 제품에 대한 자신감 ↓

##### 4.4.1 **<ins>Continuous Intergration</ins>** 

> 팀 프로젝트에서 **작업을 빈번하게 검증 및 통합** 이루어지게 하는 방법 (매일 최소한 한 번)

* **결함의 조기 발견**으로 인한 **비용 감소**
* **위험 감소**
* 제품에 대한 **자신감 ↑**

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/1d775e03-5820-472d-bff9-a2f41470620b" alt="CI" style="zoom:50%;" />

commit -> fetch changes -> build -> test -> result

*※ CI의 모든 과정이 적절한 tool chain을 통해 자동화*

##### 4.4.1 **<ins>Continuous Delivery</ins>** 

>시스템이 실제 운영 환경에서 **릴리스 될 준비**가 되었는지 확인 및 다양한 테스트 환경에서 **테스트**

##### 4.4.2 **테스팅 환경**

* (QA) Testing Environment : QA 팀이 테스트를 진행하는 환경 
  * 복잡하고 시간이 걸리는 테스트 진행
* Staging Environment : 실제 운영 환경과 동일한 환경 (최종 관문 )
  * **실제 데이터를 사용**하여 시스템을 대상으로 **사용자 인수 (UAT)**를 포함한 다양한 비기능적 테스트(**부하, 성능, 보안, 장애**) 수행
* Production Environment : 실제 운영 환경
  * 배포시 **Blue-green, Canary** 등의 배포 전략을 사용함

##### 4.4.3 Testing Pyramid

1. Unit Testing
   * **각 컴포넌트의 동작 확인**
   * 의존관계의 컴포넌트는 가짜(Test Double)로 대체
2. Intergration Testing
   * 시스템이 **외부 환경(DB, 파일 시스템, 외부 시스템)과의 통합**이 문제가 없는지 테스트
   * **의존성 테스트를 의미**
3. E2E Testing (End to End Test)
   1. **UAT(User Acceptance Test)에 같은 의미**로도 사용
   2. 전체 시스템이 통합된 상태에서 **사용자 관점으로 테스팅**

​	*※ 일반적으로 Unit -> E2E로 갈 수록 (비용 ↑, 속도 ↓ -> 테스팅 횟수 ↓)* 



##### 4.4.4 Continuous Deployment 

> 실제 운영 환경으로 배포할 때 사람의 개입없이 **자동으로 배포**

*※ Delivery의 경우 Manual Approval을 통해 사람의 승인이 필요함*



#### 4.5 배포 전략

> **Production env로 배포할 때** 서비스 중단되는 시간이 없도록 **무중단(zero down time) 배포가 중요**

*※ **문제 발생 시 rollback 필요***

###### 4.5.1 **Rolling Update**

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/9f6faa8f-57ba-43c2-ab31-f2658f147893" alt="rollingupdate" style="zoom: 67%;" />

​	```기존 인프라에 하나씩 새로운 버전으로 대체```

​	단점 

* 구버전과 새버전의 **혼재**
* 서버에 새버전으로 배포될 때 **서버 과부하 가능성** 존재

###### 4.5.2 **Blue green**

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/19c556b6-5e4f-486a-ad27-c899fd2a134e" alt="bluegreen" style="zoom:67%;" />

​	``` 두 개의 동일한 운영 환경을 준비하여 동시에 교체하는 방법 ```

단점

* **여분의 인프라** 준비 필요

장점

* 신버전 구전의 **혼재된 서비스가 없음**
* **rollback이 쉬움**

###### 4.5.3 **Canary**

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/0305448a-4c36-4eef-b2e6-00c3255ae813" alt="canary" style="zoom:67%;" />

``` 구버전의 일부 서버를 새버전으로 대체하고 일부 트래픽을 분산시킴 → 이상이 없으면 나머지 서버들도 교체함``` 

* 소수의 사용자에게만 배포되기 때문에 **blue green보다 상대적으로 영향이 적음**
* Capacity testing 수행

