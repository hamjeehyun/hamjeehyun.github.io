---
layout: post
title: 소프트웨어공학 | Chapter1. 소프트웨어 공학과 소프트웨어
hide_title: true     
date: 10 february 2020
excerpt_separator: <!--more-->
---

# 소프트웨어공학 | Chapter1. 소프트웨어 공학과 소프트웨어
<br>
<br>
<br>
<br>
## 1.1 소프트웨어 공학이 뭔가요?
<!--more-->
소프트웨어 개발에 공학적 패러다임을 적용하자는 취지로 시작되었다.   
바우어(Bauer)는 소프트웨어 공학에 대학여 다음과 같이 정의한다.  
<br>

> 기계에서 효율적으로 작동되는 신뢰성 있는 소프트웨어를 경제적으로 획득하기 위해 적절한 공학적 원리를 수립하여 활용하는 것이다.  
"Establishment and user of sound engineering principles to economically obtain software that is reliable and works on real machines efficiently"

<br>
또한 IEEE(Institute of Electrical and Electronics Engineers)는 소프트웨어 공학을 다음과 같이 정의하고 있다.
<br>

> 소프트웨어의 개발과 운용, 유지보수에 대한 체계적(systematic)이며, 훈련된(disciplined) 계량화할 수 있는(quantifiable) 접근방식의 적용이다.  
"the application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software"

<br>
<br>
<br>
## 1.2 소프트웨어에 대한 이해
솜머빌(Sommerville)의 정의
> 소프트웨어는 단순한 프로그램 뿐만 아니라 프로그램이 올바르게 작동하도록 하는데 필요한 **관련된 문서 및 설치 데이터** 를 의미한다.

<br>
프레스만(Pressman)의 정의
> 소프트웨어는  
1) 실행되면서 원하는 기능이나 함수, 성능을 제공해 주는 명령어들 (컴퓨터 프로그램)  
2) 프로그램이 데이터를 적절하게 처리할 수 있게 해 주는 **자료구조**  
3) 프로그램의 사용이나 운영을 나타내는 하드카피나 가상 형태인 문서  
이다.

<br>
기업에서 활용하는 대부분의 소프트웨어는 개발과정에서 분석과 설계를 위한 방대한 문서 산출물들이 만들어지며, 이러한 문서들은 향후 유지보수를 위해 필요한 것들이다.  
하지만 프로ㅔ스만의 정의에 따르면 데이터베이스에 저장해야 할 데이터는 소프트웨어가 아닐 수 있으며, 다른 소프트웨어로 대체될 경우 데이터는 새롭게 커스터마이징(costomizing)하여 이전되어야 할 것이다.
<br>
<br>
<br>
## 1.3 소프트웨어의 특징과 분류
#### 소프트웨어 개발이 실패하는 이유
1. 비가시성
1. 변경성
1. 복제성
1. 복잡성

<br>
<br>

#### 소프트웨어의 분류

분류 | 내용
:-------: | :---
시스템<br>소프트웨어 | 다른 프로그램의 수행을 지원해주기 위해 만들어진 소프트웨어
애플리케이션<br>소프트웨어 | 특수한 업무상의 요구를 해결해주며, 비즈니스 처리 또는 관리/기술 측면에서의 의사결정을 쉽게 할 수 있도록 사업상 또는 기술적 데이터를 처리하는 소프트웨어
공학/과학 소프트웨어 | "수 처리" 알고리즘이 특징이며, 공학 및 과학적 연구를 위해, 실시간 처리가 가능한 소프트웨어
임베디드 소프트웨어 | 생산품이나 시스템에 내장되어 있으면서 사용자나 시스템 자체를 위한 특징이나 기능을 구현하는데 사용
웹 응용시스템 소프트웨어 | 인터넷을 위해 개발된 하이퍼텍스트이거나, 웹으로 가도오디는 으용 시스템을 위한 소프트웨어
인공지능 소프트웨어 | 계산이나 일반적인 알고리즘으로 분석할 수 없는 복잡한 문제를 해결하기 위해 비수치적 알고리즘을 사용
생산라인 소프트웨어 | 제조공정과정에 필요한 소프트웨어

<br>
<br>
<br>
## 1.4 소프트웨어의 탄생과 폐기
#### 소프트웨어의 라이프사이클(life cycle)
먼저 소프트웨어를 만들기 위한 프로젝트가 착수되고 계획이 이루어진다.  
실제적인 소프트웨어의 모습이 만들어지기 시작하는 것은 프로젝트 실행단계의 분석과정부터이며, 설계과정을 통해 좀더 구체적인 소프트웨어 겉모습이 만들어진다.  
테스팅을 통해 가동이 제대로 가능한지 여부가 판가름 나게 된다.  
<br>
- 사용자 인터페이스(User interface) : 소프트웨어의 겉모습
- 로직(Logic) / 데이터베이스 구조(Database Structure) : 내부 처리
- go-live : 프로젝트가 원래 목적을 달성하기 위한 가동과 함께 살아 움직이게 되는 것을 말하는 이벤트
<br>

<img src="./assets/img/pexels/software.jpg">

<br>
<br>
<br>

### 1.4.1 Project 관리
프로젝트 관리는 PMI(Project Management Institute)에 의해 착수, 계획, 실행, 종료의 단계로 나누어진다.  

##### 착수 단계
- 소프트웨어 개발의 필요성 인식
- 예산 확보 / 입안과정
- 필요 시 외부 전문조직에게 프로젝트를 의뢰하기 위하여 REP(Request For Proposal) 제작  

##### 계획 단계
- 프로젝트 소프트웨어 개발을 위한 방법론과 구체적인 일정 수립  

##### 실행 단계
- 실제 소프트웨어 개발업무  

##### 종료 단계
- 프로젝트를 마무리 하는 과정
- 업무를 운영으로 이관  
<br>

### 1.4.2 소프트웨어 개발
소프트웨어 개발단계는 일반적으로 분석, 설계, 구현, TEST 단계로 나누어진다.  
<br>

### 1.4.3 유지보수

유지보수의 종류 | 변경의 강도 | 내용
:---: | :---: | :---:
완전유지보수 | 강 | 새로운 요구사항을 추가하거나 시스템의 구조와 성능을 개선하여 시스템을 완전하게 만드는 목적으로 수행
수정유지보수 | 중 | 요구사항의 오류나 설계 및 구현 상의 오류를 개선할 목적으로 수행함
적응유지보수 | 하 | 시스템의 플랫폼 변경과 같은 새로운 환경으로의 적응을 목적으로 수행
예방유지보수 | 하 | 시스템의 잠재적인 결함을 사전에 방지하기 위한 목적으로 수행

<br>
<br>
<br>
## 1.5 다양한 소프트웨어 도입 프로젝트
### 1.5.1 인하우스(in-house) 개발 프로젝트
조직 내부에서 자체적이니 개발인력을 활용하여 소프트웨어를 개발하는 방법이다.  
<br>

### 1.5.2 SI 프로젝트
조직 내부의 인력으로 감당하기 어려운 규모의 시스템을 구축하고자 할 때, 전문 SI업체에게 개발을 맡기는 경우이다.  
<br>

### 1.5.3 패키지 도입
패키지의 종류는 다양하며, 기업의 입장에서 세계적으로 유명한 SAP나 ORACLE 등 ERP 패키지를 도입하는 경우가 대표적이다.  
패키지는 가장 일반적인 기능을 수정 보완하여 활용할 수 있도록 커스터마이징이 가능하며, 수정해야할 수준에 따라 커스터마이징 기간이 길어지거나, 비용이 추가적으로 발생한다.
