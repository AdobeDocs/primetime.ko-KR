---
title: Roku SSO 개요
description: Roku SSO 정보
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Roku SSO 개요 {#overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## 소개 {#roku-sso-intro}

이 문서에서는 Roku 장치에서 단일 사인온 기능을 활용하는 데 필요한 정보를 설명합니다. Adobe Primetime 인증은 Roku와 협력하여 로그인 사용자 경험을 개선하고 TV 가입자를 위한 TV Everywhere 애플리케이션에서 단일 사인온을 용이하게 합니다.

이 솔루션은 Adobe Primetime 인증의 Clientless REST API를 기반으로 하므로 대부분의 프로그래머가 Single Sign On의 이점을 활용하기 위해 애플리케이션을 업데이트할 필요가 없습니다.

## Roku SSO 활성화 {#enable-roku-sso}

프로그래머 또는 MVPD가 SSO를 사용하지 않도록 설정하지 않는 한 Roku SSO는 기본적으로 사용됩니다.

각 프로그래머는 특정 통합을 위해 Roku 플랫폼에서 SSO를 활성화/비활성화할 수 있습니다.

### 프로그래머가 Roku SSO를 작동하기 위해 수행해야 하는 작업 {#make-roku-sso-work}

클라이언트 장치에서 REST API를 구현하는 프로그래머 애플리케이션의 경우 Roku SSO가 변경 없이 작동합니다. Roku OS는 Adobe Primetime 인증 끝점에 대한 요청에 대해 두 개의 HTTP 헤더를 추가합니다.

REST api에 대한 서버 간 솔루션 을 구현하는 프로그래머 애플리케이션의 경우 프로그래머는 Roku 팀에 연락하여 이 두 헤더가 모든 api 흐름의 도메인으로 전송되는 구성을 요청해야 합니다.

애플리케이션 간(및 디바이스 간) SSO를 보장하기 위해 애플리케이션에서 전달하는 장치 ID 대신 사용할 Roku 제공 구독자 ID입니다.

필요한 헤더의 형식에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

### 가능한 문제 {#possible-issues}

프로그래머는 Adobe의 Clientless REST API를 기반으로 한 현재 구현이 Roku의 platform-SSO를 방해하지 않는지 확인해야 합니다. 가능한 문제 및 해결 방법 목록은 아래를 참조하십시오.

| 문제 | 가능한 원인 | 가능한 솔루션 | |-|-| |Adobe에게 보낸 Roku SSO 헤더 없음|Adobe Primetime 인증 도메인 호출에 HTTPS 대신 HTTP 사용|HTTPS 사용| |MVPD 로고가 표시되지 않음/SSO 토큰에 대해 업데이트되지 않음|UI가 로컬 저장소에 의존함|응용 프로그램이 인증을 확인한 후 UI(및 필요한 경우 로컬 저장소)를 업데이트해야 함| |AuthZ에서 로그아웃이 트리거되지 않음|응용 프로그램 디자인을 업데이트해야 백그라운드에서 로그아웃을 수행할 수 없음|

## FAQ {#faq}

* **SSO는 어떻게 작동합니까?**

   SSO는 동일한 Roku 사용자와 연결된 모든 Roku 장치에서 Adobe Primetime 인증을 통해 제공되는 모든 프로그래머 애플리케이션에서 작동합니다.
모든 MVPD가 Roku SSO를 허용하지는 않습니다.

* **인증 TTL에 변경 사항이 있습니까?**

   첫 번째 유효한 인증 토큰은 SSO 수행에 사용되며, 이 경우 SSO를 통해 인증될 다른 모든 애플리케이션은 만료될 때까지 동일한 TTL을 사용합니다. 따라서 한 애플리케이션에서 다른 애플리케이션으로 이동할 때 두 번째 애플리케이션은 인증하는 첫 번째 애플리케이션의 TTL을 공유합니다.

* **다른 Adobe 기능이 이전처럼 작동합니까?**

   모든 Primetime 인증 기능은 이전과 동일하게 작동합니다.

* **프로그래머 옵트인/옵트아웃 프로세스가 Roku 플랫폼에서 SSO의 이점을 누리고 있습니까?**

   이는 Adobe의 TVE Dashboard에서 구성이 변경됩니다. 각 프로그래머는 특정 통합을 위해 Roku 플랫폼에서 SSO를 활성화/비활성화할 수 있습니다.
