---
title: 프로젝트
author: Kong seonui
date: 2022-12-27
category: Portfolio
layout: post
---

이벤트 앱 리뉴얼
-------------
<p>
<img src="https://user-images.githubusercontent.com/108510080/176999987-0a86ba87-431f-4ee8-9bc0-e751bb239c22.PNG" width="240"  alt="image">
<img src="https://user-images.githubusercontent.com/108510080/176999994-2ab770ed-12b5-4aee-a1be-c9f0d7b89d21.PNG" width="240"  alt="image">
<img src="https://user-images.githubusercontent.com/108510080/176999996-8592e70c-60ed-4160-84b3-813639e2df2e.PNG" width="240"  alt="image">
<img src="https://user-images.githubusercontent.com/108510080/176999998-abdd8a32-0654-4e56-b897-1f7e9274f2e7.PNG" width="240"  alt="image">
<img src="https://user-images.githubusercontent.com/108510080/176999999-4b3c5b3c-1349-40ba-a426-7caffbb5729a.PNG" width="240"  alt="image">
</p>

<!--break--> 

- 사용 기술:
 Swift, WebKit, UIKit
- 프로젝트 설명:  
 사용자들이 이벤트에 참여할 수 있도록 하는, 이벤트가 있는 경우 푸시 알림도 받을 수 있는 앱입니다.  
 웹 페이지를 리뉴얼하며 hybrid앱인 해당 앱도 함께 리뉴얼 하였습니다.  
 각 서비스 담당 개발자들과 협업하며 웹뷰 관리, 로그인/로그아웃 관리, 공유하기, PUSH알림, 인앱브라우저, Firebase Analytics, Firebase Crashlytics 기능을 변경 혹은 추가 하였습니다.  
 ObjectvieC로 구현 되어있던 코드를 전부 Swift 개발언어로 전환 하였습니다.

- 핵심 기능 구현 방식:  
 1. 기존 ObjectiveC로 구현된 코드를 Swift 구조에 적합하도록 리펙토링 해주었습니다.
 2. 웹뷰: 앱에서의 웹 UX를 구현해주었습니다. 웹의 액션을 인지하기 위해 trigger가 필요했고, 이를 스키마 호출로 해결하였습니다. 
    앱에서는 이 스키마가 오면 웹에서 필요한 동작(뒤로가기, 앞으로가기, 얼럿노출, 새창노출 등)을 구현해주었습니다.
 3. 로그인/로그아웃: 로그인시 앱에서 스키마를 받아 쿠키를 구워 저장해 세션 유지가 가능하도록 하였습니다. 로그아웃 액션이 있을시 쿠키를 제거하였습니다.  
    앱에서의 로그아웃인 경우 스크립트를 통해 웹에 액션을 알렸습니다.
 4. PUSH알림: Firebase Cloud Message을 적용하였습니다. 앱에서는 푸시권한과 수신정보 전달을 처리하였으며, APNS에서 수신한 Notification이 오면 이벤트 페이지로 이동하는 기능을 앱에서 구현하였습니다.
 5. 인앱브라우저: 상품정보 페이지 부터 결제까지 진행되도록 설계되었습니다. 다른 쇼핑몰 이동과 쇼핑몰에서의 앱결제가 가능하도록 whitelist에 앱스키마 추가를 해줬습니다.  
 6. Firebase 라이브러리를 사용해 Firebase,Analytics, Crashlytics를 추가하여 효율적인 이벤트 관리와 충돌 관리가 가능하도록 하였습니다.

- 느낀점:  
입사 이후 처음 많은 개발자들과의 협업을 했던 프로젝트입니다.  
또한 리뉴얼 내용 뿐만 아니라 ObjectiveC에서 Swift로 통째로 언어 전환을 한 앱이기 때문에 내부테스트 혹은 전수테스트 등 많은 테스트를 거쳤던 프로젝트입니다.  
기존에 유지보수를 통해 웹뷰를 관리해왔었지만, hybrid앱의 web과의 소통과 앱에서의 역할을 더욱 잘 이해할 수 있었습니다.  
처음 배포했을때 메모리 문제로 예상치 못한 몇개의 충돌이 있었고, 이를 해결하며 추후 작업시에 메모리 누수 관리에 대해서 더 신경쓰게 되는 계기가 되었습니다.   
Firebase 여러 제품을 연동해 보며 추후 어떤 상황에서 유용하게 적용해 볼수 있을까도 생각해 보게 되었습니다. 
