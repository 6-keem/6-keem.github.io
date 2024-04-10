---
title : "[소프트웨어 공학] UML: Class, Sequence, Package Diagram"
date : 2024-04-10 23:11:00 +0900
categories : [소프트웨어 공학, 정리]
tags : [software engineering] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

## 1. Class Diagram

* 문제나 해결책의 **정적인 구조 표현**

* 클래스와 **그들간의 관계 표현**

시스템의 내부 구조를 나타냄



### 1. 클래스

* UML의 클래스 표현

  * 세부분으로 나누어진 박스로 표현
  * <ins>클래스 이름</ins>(필수) / 속성 / 연산

  ![class](https://github.com/6-keem/BlogImageRepository/assets/113224939/1cb95c3e-8402-4d64-8841-a859dcd2a1c1)

​	※ visibility (접근제어자) : (-) private (+) public (#) protected (~) package

​			![class2](https://github.com/6-keem/BlogImageRepository/assets/113224939/c98e77cb-4897-456e-8f88-df74f537eae6)

* 반환형 : [0..*] -> (0개 이상), void -> 반환 안함
* 초기 값 지정도 가능 : - 주소:String = "서울특별시 ..."
* <ins>+평균회원구매액():Money</ins> -> <mark>static</mark>

UML = 건물 설계 (평면도, 입면도, 투시도, 조감도 등 다양한 관점에서 표현)

※ UseCase Diagram : 시스템을 블랙박스로 보고, 내부 구조는 표현하지 않는다. (집 내부를 보여주지 않는다.)



### 2. 관계

#### 1. 연관관계 (Assosiation)

##### 클래스 (실선, 화살표 가능)

* 개념상 서로 연결 / 역할, 연관관계 이름 명시 (선택)

* r1,r2 -> 역할 m1,m2 -> 다중성 / 연관 관계는 클래스의 속성으로 구현 (참조 가능)

* 다중성 해석 시 ~~클래스~~ **인스턴스** 관점으로 해석

* 양방향 연관 관계 
  * 서로의 존재를 인지 / 클래스 ------ 클래스
* 단방향 연관 관계
  * 한 쪽만 존재 인지 / 클래스 -----> 클래스

##### 인스턴스 (실선, 화살표 X)

* **갑돌이는** **마스크를** 2020년 4월 10일10장 주문했다.
  * 갑돌이 - 고객 , 마스크 - 제품 (이름 생략 가능)

* Instance Assosiation 
  * 객체 간의 관계 - <mark>link (연관관계 X)</mark>라고 한다
* **객체간의 관계를 파악**하여 객체 다이어그램 **작성 후** 클래스 다이어그램 작성도 가능

##### 연관 클래스

* 연관 관계 이름으로



#### 2. 일반화 관계 (Italic or guillemets) - extends

* 일반화는 is a kind of 관계 (가전제품(추상클래스) - 식기 세척기, 냉장고 ...)

※ **(Guillemets)** - UML을 새로운 개념을 반영하여 확장하는 매커니즘 -> <mark>Stereotype</mark>



#### 3. 집합 관계 - 전체와 부분간의 관계

* **aggregation(집약)** - 약한 결합
* **composition(합성)**  - 강한 결합



#### 4. 의존 관계 

한 클래스에서 다른 클래스를 사용하는 경우

* 클래스의 속성에서 참조
* 연산의 인자로 참조
* 메소드의 지역 개체로 참조

지속적 관계 - 실선 화살표

찰나의 관계 - 점선 화살표



#### 5. 실체화 관계 - guillemet, implement

* <ins>인터페이스란 계약</ins>이다
* 인터페이스 - 클래스사이는 점선

* provided interface 클래스가 사용하는 인터페이스를 rquired interface를 사용하여 모델링

인터페이스 사용 장점

- 서비스 제공 클래스가 변경되도 서비스 사용 클라이언트 코드 영향 X



## 2. Object Diagram

* 클래스 다이어그램의 인스턴스 (사례를 보여줌)

클래스 추출

속성 추출

클래스 간 관계 추출

![objectDiagram](https://github.com/6-keem/BlogImageRepository/assets/113224939/05083121-771f-4bb2-8243-028a85925e1e)

## 3. Sequence Diagram

Class Diagram : 구조 모델링

Sequence Diagram : 행위 모델링

전체 시스템을 나타내는 클래스는 제외

| 순차 다이어그램                                              | 프레임과 결합 프레그먼트                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/4fefc1f5-4cc5-44da-ba9e-b6179e9db44f" alt="sequencediagram" style="zoom:67%;" /> | <img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/8c06634c-2cb1-407f-9848-de42b61fb397" alt="frame" style="zoom:80%;" /> |

* Activation (활성구간) , Return 생략할 수 있다.

* Selft Message - 자기 자신 호출

![operator](https://github.com/6-keem/BlogImageRepository/assets/113224939/f13ce07e-efaf-4c65-a662-c62a0679bece)



## 4. Package Diagram 

* 클래스 같은 여러 요소 그룹화 가능
* 모든 요소 하나의 패키지에만 존재 가능
* 패키지는 namespace 가진다 (같은 클래스 이름 다른 패키지에 존재 가능)
* 패키지 제거시 내부 모든 요소 제거됨

### 패키지 관계 

* 의존 관계 존재

![packagediagram](https://github.com/6-keem/BlogImageRepository/assets/113224939/52a5b1b6-7045-42f9-a7a6-2f54795ab563)

​							 A에서 B패키지의 요소 사용

* B 패키지 변경 시 A에게 영향을 끼침 (반대는 성립하지 않음)
* A패키지를 B패키지 없이 단독 재사용 불가능

![packagediagramimport](https://github.com/6-keem/BlogImageRepository/assets/113224939/dfa3aee2-2612-402d-94e6-88206bfed9c3)
