---
title : "[소프트웨어 공학] Prototype, UML:Use Case Modeling"
date : 2024-04-05 23:23:00 +0900
categories : [소프트웨어 공학, 정리]
tags : [software engineering] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

# Prototype

---

## 1. 프로토 타입

* 시스템 일부 경험할 수 있는 도구
* 요구 사항의 대화 촉진, 오류나 누락 식별
* stakeholder가 시스템 요구사항에 대한 이해 ↑

* 요구사항 도출/분석/검증 도구로도 사용



### 프로토 타입 종류

#### 범위(Scope)에 따른 분류

* Horizontal prototype

  - UI Prototype

  * User Interface (FE)만 구현
  * 오류 처리 미비
  * <ins>요구사항 구체화 등에 좋음</ins>

* Vertical prototype - 특정 기능 (실제 동작)
  * 기술적 타당성 평가 목적으로 PoC(Proof of Concept, 개념 증명)

#### 충실도(Fidelity)에 따른 분류

Fidelity : 최종 제품과 흡사한 정도 (**<ins>Visual Design, Content, Interactivity</ins>**)

* Lo-fi(Low Fidelity) prototype -Balsamiq
* Hi-fi(High Fidelity) prototype

| Fidelity | Visual Design                               | Content                                                     | Interactivity                            |
| -------- | ------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------- |
| Low      | 상세 부분 생략 최종 제품의 일부 시각적 속성 | 콘텐츠 주요 요소만 / 가짜이거나 하드 코딩                   | Paper prototyping / Clickable Wireframes |
| High     | 사실적이고 상세한 디자인                    | 실제 또는 실제와 유사한 컨텐츠 / 최종 설계의 일부 또는 전부 | 최종 제품과 비슷한 수준으로 상호작용     |

### 그 외 분류

#### Throwaway 프로토 타입

* 일회성으로 목적 달성 후 폐기
* ~~견고성, 신뢰성, 성능~~ -> **빠른 구현과 수정**

#### Evolutionary 프로토 타입

* 진화형으로 제품을 **점진적 개발**
* 엄격한 개발과정 적용



### Paper Prototyping (Lo-fi)

<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/eb1ece11-c3d5-4243-ac89-3b9e7221bfe3" alt="paperprototyping" style="zoom:67%;" />

​	**요구사항 도출 및 요구사항 검증이 가능함**

## 2. UML : Use Case Modeling

*※ Unified Modeling Language*

**Structure Diagram, Behavior Diagram 존재**

* 요구사항 분석 -> 분석 모델

  요구사항 모델링

* 설계 -> 설계 모델

​	해결책을 모델링

### 2.1 모델의 역할

* 서로의 해석 공유 및 합의하여 해석의 타당성 검토
* 현재 또는 앞으로의 시스템 원하는 모습으로 가시화
* 시스템을 구축하는 틀 제공

*요구사항 표현*

* *사용자 스토리 (Scrum)*
* *<mark>Use Case Diagram</mark> (UML)*



### 2.2 Use Case Diagram

* 사용자 관점에서 기술하여 사용자와 시스템 사이의 상호작용 보여줌
* 제공 기능, 서비스 정의, 시스템 범위 결정

<ins>**※ 유스케이스란 시스템을 사용하는 목적이다.**</ins>

#### 2.2.1 구성요소

![usecasediagram](https://github.com/6-keem/BlogImageRepository/assets/113224939/64ddbc0c-f432-46f4-b562-0cfe5a9c94f1)

#### 시스템 System

* 만들고자 하는 어플리케이션
* 유스케이스를 둘러싼 사각형 틀을 그리고 시스템 명칭을 사각형 안쪽 상단에 기술
* **<ins>시스템의 범위를 표시</ins>**

#### 액터 (Actor)

* 시스템 외부에 존재하며 시스템과 상호작용 하는 사람 또는 다른 시스템

#### 유스케이스 (UseCase)

* 시스템이 액터에게 제공해야 하는 기능의 집합
* 시스템의 요구사항 보여줌

#### 관계 (RelationShip) - <ins>표현법 확인</ins>

* Actor <-> UseCase 사이의 의미 있는 관계

* 연관 관계 (association)

* 의존 관계 (dependency)

  * 포함 관계 (include) - 표현법 : <mark><ins>**UseCase << include >> UseCase**</ins></mark> (<< >>)

  * 확장 관계 (Extend) - 선택적 관계

    *※ 반드시 ~~ 해야한다는 포함관계 *

* 일반화 관계 (generalization)

*※ 구체적인 상호작용은 유스케이스 명세서에 기술*



### 3. UseCase Diagram 작성 순서

![usecase](https://github.com/6-keem/BlogImageRepository/assets/113224939/bbabea1f-4d01-4f6d-b7a5-505b7b760bab)

#### 유스케이스 명세서 작성

* 액터가 유스케이스로 표현된 목적을 달성하기 위한 시스템과 상호작용하는 단계 기술



primary actor (주 액터) : 시스템을 사용하여 실제 가치를 얻는 액터

* UseCase Diagram의 왼쪽에 그리는 것이 관례

Secondary actor  : primary actor가 목적 달성을 위해 지원하는 액터

* 오른쪽에 나타냄



<img src="https://github.com/6-keem/BlogImageRepository/assets/113224939/a0c4e02d-26c7-486a-a39a-a7075a179fde" alt="usecaserelationship" style="zoom:67%;" />



----





## 실습) Bulletin Board Usecase Diagram

![usecasediagramexercise](https://github.com/6-keem/BlogImageRepository/assets/113224939/818f5e2f-5df9-4718-bcb2-65c7266587ec)