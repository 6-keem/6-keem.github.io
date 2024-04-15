---
title : "[소프트웨어 공학] Coupling and Cohesion"
date : 2024-04-15 22:44:00 +0900
categories : [소프트웨어 공학, 정리]
tags : [software engineering] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

## Coupling and Cohesion (결합도, 응집도)

### 설계의 기본 원칙

* Cohesion : 관련된 것을 묶는 것 **(높게 설계)**

* Coupling : 모듈관의 관계 **(낮게 설계)**

![응집도결합도](https://github.com/6-keem/BlogImageRepository/assets/113224939/41dfadd3-4b30-4a95-8d6f-45f9e9b4b145)

※ A, B : 모듈 (응집도와 관련) / A <-> B : 모듈관의 관계 (결합도) 

### 1. CoheSion (응집도) 

Cohesion : 한 모듈을 구성하는 코드가 관련 있는 Element로 묶였다. 

Element : 한 코드 안에 있는 함수 

한 기능을 수행하는 모듈의 응집도 > 여러 기능 수행하는 모듈의 응집도

![cohesion](https://github.com/6-keem/BlogImageRepository/assets/113224939/56396892-1d8e-47d3-9362-6de82915441e)

|                         응집도 높음                          |                         응집도 낮음                          |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| Functional (기능적) <br>Sequential (순차적)<br>Communication (통신적) | Procedural (절차적)<br>Temporal (시간적)<br>Logical (논리적)<br>Coincidental (우연적) |

가능한 하나를 위한 기능만 담아야함

#### 응집도 판단

![cohesion2](https://github.com/6-keem/BlogImageRepository/assets/113224939/56674057-d2c7-42ad-80fb-e0854e8eb6cd)

※ Communication - 동일한 데이터를 이용 

#### Functional Cohesion

* 여러 코드들이 하나의 기능을 수행 (한 코드 제거하면 기능 수행 불가능)

* 코사인 값 구하는 모듈, 비밀번호 검증 모듈 등

##### Advantage

* Easy to maintain
* Easy to understand
* Black Box (내부 구조 몰라도 사용할 수 있음) - 다른 챕터에 어디에 사용됐는지



#### Sequential Cohesion

* 모듈 안에 있는 함수들이 데이터로 연관 (출력 값이 입력 값이 되는 등)
* 순이익 계산 (파운드) -> 파운드 달러로 변환

→ Functional Cohesion으로 분리할 수 있는지? (코드 재사용을 위함)



#### Communication Cohesion

* 동일한 데이터로 여러 기능 수행
* 고객 계좌를 통해 -> 고객의 이름 조회, 고객의 잔액 조회



---

### Modularity Line

---



#### Procedural Cohesion

* 데이터 관련은 없지만 실행 순서 Control (여러 기능)
* 비행 경로 추적 -> 알람 활성화



#### Temporal Cohesion

* 초기화 하는 init 함수 (시점과 관련)
* 특정 변수만 초기화하고 싶을 때 (문제 발생가능)



#### Logical Cohesion

* 논리적 유사성이 있을 경우
* flag 값에 따라 (miles → kms / kms → miles)
* f**lag 값에 따른 의미를 알아야 사용할 수 있음**



#### Coincidental Cohesion

* 관련 없음 (Dollar → Pounds / Kms -> miles)



---



### 2. Coupling (결합도)

* 결합도(의존성)는 낮게 설계하는 것이 목표

* A가 변경되면 B도 변경해야 하는 경우

![coupling](https://github.com/6-keem/BlogImageRepository/assets/113224939/6abda5b9-792f-4725-8572-7afd7de6fa3e)

|                       Normal (Good)                       |                  Poor                   |
| :-------------------------------------------------------: | :-------------------------------------: |
| Data Coupling <br>Stmap Coupling <br>Control Coupling<br> | Common Coupling<br>Content Coupling<br> |



| <img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/ba2ce501-d51c-4f0c-9965-52b97263864f" alt="coupling2" style="zoom:67%;" /> | 박스 : Module <br/>선 : 호출<br/>0-> : Data Couple<br/>모듈 간의 호출 관계 나타내는 것 structure chart |
| :----------------------------------------------------------: | :----------------------------------------------------------: |



#### Data Coupling

* parameter로 communication
* 데이터가 기본 자료형
* B가 변해도 A는 상관 없음



#### Stamp Coupling

* 데이터가 구조체일 때 *(구조체의 일부분의 데이터만 필요할 때 다른 부분은 필요 X)*

* 랜트카 예시
  * 기본 요금 - 차량 종류, 운전 거리
  * 교통 요금 - 운전 거리

※ Recompilation 필요함

-> 필요한 정보만 전달하면 해결할 수 있음



#### Control Coupling - Flag

* 안 쪽이 채워진 Data Couple 모양으로 나타냄

* Flag를 따라서 다른 기능을 수행할 때

*※ B에서 Flag에 따라 다른 기능을 수행할 때 A에서도 Flag 값의 의미를 알아야 함*

*※ 함수를 나누면 Data Coupling으로 바꿀 수 있음*

*※ 논리적 응집도는 Cotrol Coupling 과 연관이 깊음*





---

### Modularity Line

---

#### Common Coupling

* 전역변수 사용 시

#### Content Coupling

* 어셈블리 언어