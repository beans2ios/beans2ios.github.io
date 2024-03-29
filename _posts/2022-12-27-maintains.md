---
title: 유지보수
author: 공선의
date: 2022-12-27
category: Portfolio
layout: post
---

ObjectiveC to Swift 개발 언어 전환
-------------
<p>
 <img width="480" alt="image" src="https://github.com/beans2ios/beans2ios.github.io/assets/108510080/3164925c-b765-4310-8f59-62dba7b0ad73">  
</p>


### 주요 사용 기술
ObjectiveC, Swift  

### 기능 설명
Native, Hybrid 앱의 ObjectiveC로 구현된 코드를 Swift로 전환했습니다.  

### 구현 방식
전체 코드 내용이 방대하며, 오류발생의 문제가 있을 수 있다고 판단되어 기능 단위로 전환했습니다.  
리펙토링 및 Swift 대략적인 전환 과정은 다음과 같이 진행했습니다.  

1. 변경하고자 할 기능 단위의 코드의 종속성 분리가 가능한지 확인  
2. Swift 적용이 가능한 기능인지 확인  
3. 약속된 디자인 패턴 적용한 틀을 새로운 프로젝트에서 생성. (대체로 이벤트나 API 통신이 필요한 기능은 MVVM, 단순 뷰 노출은 MVC로 구현)  
4. Storyboard, xib로 생성한 뷰를 코드로 변환  
5. 네트워킹이 있다면 dummy Data 생성하여 테스트  
6. 변경할 기능을 새로운 프로젝트에서 Swift로 코딩  
7. 구현한 코드를 기존 코드에 결합  

### 느낀점  
Swift 언어의 공부를 막연히 Playground에서 하는게 아닌 실전에서 적용해 보는 큰 경험이 되었습니다.  
개발 언어 전환한다는 것에 의미를 두지 않고 처음부터 깔끔하게 코드를 짜려면 어떻게 하고 추후 유지보수를 용이하게 하려면 어떻게 할 것인가?를 생각하며 작업하다 보니 코드의 설계나 디자인 패턴 적용이나, 기능을 수행하는 Class의 분리 등 학습하고 적용할 수 있는 경험이 되었습니다.  

상세 검색 기능 변경
-------------
<p>
 <img width="240" alt="image" src="https://user-images.githubusercontent.com/108510080/176878469-988749d2-937f-45d5-90ae-fc6450c3a0a5.PNG"> 
 <img width="240" alt="image" src="https://user-images.githubusercontent.com/108510080/176878484-ba6f3b82-d603-443d-8d26-a941a075f102.PNG">
 <img width="240" alt="image" src="https://user-images.githubusercontent.com/108510080/176875174-c344e1a0-85f8-4409-8419-cbc0937b05b3.png">  
</p>

### 주요 사용 기술
Swift, UIKit  
  
### 기능 설명
상세검색 기능을 변경 해달라는 요청을 받았고, 추가로 기존의 ObjectiveC로 구현된 코드를 리펙토링 해주었습니다.  
크게 테이블뷰와 컬렉션뷰, 스택뷰와 스크롤 뷰를 사용하여 사용자에게 UI를 노출시켰습니다.  
코드 구현방식은 MVC 패턴으로 구현하였습니다.
 
### 구현 방식
기존 코드는 ObjectiveC로 구현되었을 뿐 아니라, 모든 뷰가 하나의 뷰컨트롤러에 종속되어 있는 God Class로 구현되 있던 코드였습니다.  
이 종속성을 없애고자 사용자에게 제공되는 뷰를 나눠 총 5개의 뷰와 1개의 뷰컨트롤러로 나눠 생성해 주었습니다.    
사용자에게 보이는 뷰는 크게 5가지인데,  
1. 왼쪽의 카테고리 Item들이 노출되는 뷰  
2. 키워드와 가격대를 검색할 수 있는 뷰  
3. 왼쪽 카테고리의 Item의 선택에 따라 보이는 2 depth 카테고리 Item들이 노출되는 뷰 
4. Item이 선택되었을 때 선택된 Item이 보이는 뷰  
5. 초기화와 적용 버튼이 들어가 있는 하단 뷰  
입니다.  
그리고 5개의 뷰를 연결해 주는 뷰컨트롤러를 1개 추가 생성해 주었습니다.
 
기존 코드의 GodClass에 종속되어 있던 Network 역할을 하는 service 클래스를 따로 빼주었습니다.  
네트워크 3-party 라이브러리가 변경되는 경우에 코드 변경을 최소화할 수 있도록 의존성 주입 클래스를 생성해서 Network Class를 만들어 사용해 주었습니다.  
네트워크 통신으로 받아온 json 데이터는 Codable을 사용하여 파싱 하여 model을 관리하였습니다.  
 
### 느낀 점
추후 유지보수에 대해서 고민을 하게 된 작업이었습니다.  
변경 전 코드는 하나의 뷰 컨트롤러가 왼쪽 카테고리뷰, 오른쪽 옵션뷰, 상단 선택된 옵션뷰, Network를 모두 관리하는 구조였습니다.  
때문에 종속된 부분이 많아 유지보수가 힘들고 단위 기능의 재사용이 힘들다고 생각되었습니다.  
하여 뷰단위 기능에 대해서는 각 뷰마다의 모델-뷰-뷰컨트롤러를 분리하는 방식을 적용하였으며 "어떻게 해야 추후 유지보수 시 기능의 재사용이나 기능 추가, 기능 제거에 대한 대처가 더 쉬울까?" 생각을 해보게 되었습니다.  
네트워크 또한 의존성 주입이 가능하게 해 추후 방식이 변경될 경우에 코드 변경 대처가 쉽도록 고려해 보았습니다.  
Network와 모델 간의 동작을 간결하게 하는 방식을 생각해 보게 되었습니다.


재입고 알림 기능 추가
-------------
<p>
 <img width="240" alt="image" src="https://user-images.githubusercontent.com/108510080/177004333-c85a3bc5-a0c6-4d21-baac-4c2f50e01c79.PNG">  
 <img width="240" alt="image" src="https://user-images.githubusercontent.com/108510080/177004341-3b3cdcfb-9372-4749-b71c-9d230f309a9f.PNG">  
</p>

### 주요 사용 기술
Swift, ObjectiveC, UIKit  
  
### 기능 설명
품절 상품에 대해서 사용자가 "재입고 알림 받기"를 설정할 수 있고, 재입고되었을 때 알림을 받아 재입고 알림 상품의 상태를 확인하거나 구매할 수 있는 기능입니다.  

### 구현 방식
앱에서 재입고 설정을 한 사용자의 정보를 서버에 전달해 주고, 서버에서 푸시 알림을 보내면 apns의 notification이 오면 재입고 알림 내역을 받아와서 노출해 주었습니다.  
재입고 알림 내역은 UITableView로 노출하였으며, 재입고 상품 추가, 삭제, 변경, 조회 등은 OpenApi를 사용하여 서버와의 통신하였습니다.  
조회된 데이터는 Codable 사용하여 API로부터 가져온 데이터를 파싱 하여 model 관리하였습니다.  
재입고 알림 내역 기능에 대한 부분은 Swift로 코딩하였으며, ObjectiveC로 되어있는 코드에서도 겸해서 사용할 수 있도록 구현하였습니다.

### 느낀 점
APNS, 사내 푸시시스템, 디바이스 기기간의 푸시 전송 로직을 공부하고 더 이해할 수 있었습니다.  
그리고 "서비스의 UX의 중요성"에 대해 새롭게 정의할 수 있는 계기가 되었습니다.
작업을 하여 앱이 현재 화면에 노출되고 있는 상태인 "active 상태에서의 푸시 알림이 오는 경우"에 대해 고민해야 할 경우가 있었고,
앱이 실행 중인 상태에서는 애플에서 제공하는 푸시 알림 배너가 노출되지 않다는 것에 대해서 놀랐습니다.  
그 이유는 항상 카카오톡을 이용할 때 채팅 중에 너무나 자연스러운 상단 푸시 배너가 노출되고 있어 익숙해져 있었기 때문입니다.  
플랫폼이 아닌 서비스가 사용자의 UX를 변화시킬 수도 있구나라는 생각이 들었고, "내가 제공하는 서비스가 사용자들에게 영향을 줄 수 있겠다"는 기대감과 책임감이 생가는 계기가 되었습니다.  

배너 기능 추가
-------------
<p>
 <img width="300" alt="image" src="https://github.com/beans2ios/beans2ios.github.io/assets/108510080/6ed4e537-3552-4cf0-ab18-caaa871400b1">
</p>

### 주요 사용 기술
Swift, Paging, Timer, Thread

### 기능 설명
페이징 가능한 배너 기능을 구현했습니다.  
기본적인 페이징 구성은 자동페이징이 가능하며, 여러 개의 배너가 노출되는 경우 버튼에 의해 재생과 멈춤이 가능합니다.  
페이지를 누르면 해당 배너 정보에 포함된 URL이 웹뷰로 노출됩니다.  


### 구현 방식
페이징은 ScrollView를 이용해서 구현해 주었습니다. 
여러 개의 배너 뷰를 만들어주고, scrollView의 contentSize를 배너뷰의 개수 * scrollView의 너비로 잡아주었습니다.  
scrollView의 isPagingEnabled를 true로 설정해 줘서 scrollView가 Paging이 가능하도록 해주었습니다. 
NSTimer를 사용해서 Auto Paging을 구현했습니다. 해당 뷰가 노출되는 경우 자동으로 설정한 시간이 지나면 paging이 되는 기능입니다.  
배너의 페이징이 전후로 무한으로 동작하게 해 주었습니다. 마지막 배너가 노출되는 경우 우측으로 페이지 전환 시 마지막 배너 노출되고 첫 번째 배너가 노출되는 경우 왼쪽으로 페이지 전환 시 처음 배너 노출 처리해 주었습니다.  

### 느낀 점
자동 페이징되는 배너 노출 방식에 대해서 궁금했고 앱에서 구현 방식에 대해서 생각해 볼 수 있었습니다.  
Timer에 대해 공부하며, UI의 업데이트 및 Run Loop 동작 등 iOS에서 Thread 처리 로직에 대해 정리하는 계기가 되었습니다.  
또한, ScrollView의 구성과 Paging을 위한 contents를 넣어주는 방식에 대해서 이해를 할 수 있었습니다.

앱 성능 높이기
-------------
### 주요 사용 기술
ObjectiveC, Swift, Firebase, Xcode Instruments Tool, Debounce

### 기능 설명
앱의 성능 높이기에 대한 고민을 하고 적용했습니다. 
1. 충돌 관리
2. 메모리 누수 체크
3. api 호출 감소 고민 및 개선

### 구현 방식
1. 충돌 관리  
자체적으로 더 구체적인 충돌 코드 추적을 위해 Firebase Crashlytics를 모든 서비스 중인 앱에 적용했습니다.  
적용 후 버전의 충돌 발생을 모니터링하고, 충돌이 발생하지 않는 사용자의 비중을 99.9퍼센트 이상으로 유지했습니다.   
매달 1회 충돌을 분석하고 원인을 찾아 충돌 리포트를 만들어 관리했습니다.  
충돌 관리 모니터링으로 인해 점진적 배포를 해준 앱에 대해서 충돌 발생을 배포 초기에 발견하고 처리해줌으로써 다수의 사용자에게 영향이 갈 뻔한 오류를 사전에 예방한 적이 있습니다. 
  
2. 메모리 누수 체크  
작업 시마다 메모리 누수가 있는지에 대한 체크를 진행하고 있습니다. 
deinit 호출 체크와 Xcode Instrumnets의 Leak 도구를 사용해 메모리 누수를 체크를 하고, 자체적으로 내부테스트시에 메모리 체크리스트를 넣어줘 메모리 누수를 체크하고 있습니다.  
항시 코드를 작성할 때 메모리 누수가 의심되는 곳에 약한 참조를 걸어주고 있습니다.  
 
3. api 호출 감소 고민 및 개선  
api 호출을 줄일 수 있는 방법을 생각해 보고 감소한 경험이 있습니다.  
코드를 분석하고 앱이 실행될 때, 뷰가 노출될 때, 이벤트가 발생되었을 때 데이터가 호출되어야 하는 부분을 분석하고 호출이 낭비되는 부분을 수정했습니다.  
가장 기억에 남는 개선은 검색 이벤트시 Debounce라는 개념을 적용시킨 작업입니다.  
앱에서의 키워드 검색 시 키워드 자동완성 기능이 있었습니다. 글자가 변경될 때마다 이벤트를 감지해 api통신을 해줘 서버에서 자동완성 키워드 리스트를 가져와 노출해 주는 기능입니다.  
매번 글자가 변경될 때마다 이벤트를 감지하는 부분이 효율성이 떨어진다고 판단했습니다. 그래서 글자 변경 이벤트가 발생하고 0.3초 이내에 이벤트가 없는 경우, api호출과 자동완성 키워드 리스트를 가져와 노출하는 동작을 실행시켰습니다.  
이로 적용함으로써 1/4 이하의 api 호출 감소함으로써 서버의 부하는 감소시키고 앱 내 성능은 증가시켰습니다.  
<p>
 <img width="240" alt="image" src="https://github.com/beans2ios/beans2ios.github.io/assets/108510080/519df4e0-e6cc-416c-81a5-be74655ad467">
 <img width="240" alt="image" src="https://github.com/beans2ios/beans2ios.github.io/assets/108510080/c2ed2cbc-6533-4ee9-9255-9e3ea5b4f4f6">
</p>
(Debounce 적용 테스트 시 이벤트 감소 비교 사진)

### 느낀 점
앱 성능 개선에 대해 생각해 보는 계기가 되었습니다.  
충돌 관리 전에는 충돌 데이터도 Apple connect의 옵트인에 한정한 사용자에 대한 데이터였으며 뚜렷한 충돌 원인과 비중을 알 수 없었습니다.  
Firebase Crashlytics를 적용하고 정확한 사용자의 충돌을 한눈에 확인할 수 있었고, 팀원 간의 시각화된 차트와 정확한 비중으로 충돌에 대한 문제와 원인과 해결방식을 설명할 수 있었습니다.  
이를 토대로 충돌 관리를 해서 배포한 앱에서 전체의 0.2퍼센트의 충돌을 줄일 수 있었습니다.  
또한 충돌을 줄이고 낮게 유지하는 것도 뿌듯했지만, 실시간 모니터링으로서 많은 사용자에게 배포되기 전에 급격히 발생한 충돌을 감지해 예방한 뿌듯했던 경험이 기억에 남습니다.  

메모리 누수 체크를 통해 관련 내용을 학습하고 정리하면서 앱의 메모리 관리에 대해 공부할 수 있었습니다. 메모리의 저장 방식과 메모리 누수가 일어나는 원인과 Swift의 메모리 관리 방식등 평소에 궁금했지만 어려웠던 개념을 알게 된 계기가 되었습니다.  

api 호출 감소 고민과 이를 개선하는 작업은 사실 api호출의 성능 개선을 위해 시작한 것이었지만, 사실상 이벤트 발생과 동작 낭비를 줄이는 것에 대해서 생각해 본 계기가 되었습니다. 또한, 알지 못했던 기술들을 앱 효율을 증진을 목적으로 찾아보며 새로운 기술들을 찾을 수 있었고 계속해서 알지 못했던 기술들을 학습하고 서비스에 적용할 필요성을 느끼게 되었습니다.
