---
title: Roku SSO 개요
description: Roku SSO 정보
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Roku SSO 개요 {#overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#roku-sso-intro}

이 문서에서는 Roku 장치에서 Single Sign On 기능을 사용하는 데 필요한 정보를 설명합니다. Adobe Primetime 인증은 Roku와 협력하여 TV 구독자를 위한 TV Everywhere 응용 프로그램에서 로그인 사용자 환경을 개선하고 단일 사인온을 용이하게 합니다.

이 솔루션은 Adobe Primetime 인증의 Clientless REST API를 기반으로 하므로 대부분의 프로그래머가 Single Sign On을 통해 애플리케이션을 업데이트할 필요가 없습니다.

## Roku SSO 활성화 {#enable-roku-sso}

Programmer 또는 MVPD 요청이 SSO를 비활성화하지 않는 한 기본적으로 Roku SSO가 활성화됩니다.

각 프로그래머는 특정 통합을 위해 Roku 플랫폼에서 SSO를 활성화/비활성화할 수 있습니다.

### Roku SSO가 작동하려면 프로그래머가 어떻게 해야 합니까? {#make-roku-sso-work}

클라이언트 장치에서 REST API를 구현하는 프로그래머의 애플리케이션의 경우 Roku SSO가 변경 없이 작동합니다. Roku OS는 모든 요청 시 Adobe Primetime 인증 종료 지점에 두 개의 HTTP 헤더를 추가합니다.

REST api를 위해 서버 간 솔루션을 구현하는 프로그래머의 애플리케이션의 경우 프로그래머는 Roku 팀에 연락하여 이러한 두 헤더가 모든 api 플로우에서 도메인으로 전송될 구성을 요청해야 합니다.

애플리케이션이 전달하는 장치 ID 대신 Roku에서 제공하는 가입자 ID를 사용하여 애플리케이션(및 장치 간) 간 SSO를 보장합니다.

필요한 헤더의 형식에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

### 가능한 문제 {#possible-issues}

프로그래머는 Adobe의 Clientless REST API를 기반으로 하는 현재 구현이 Roku의 platform-SSO를 방해하지 않는지 확인해야 합니다. 가능한 문제 및 해결 방법이 나와 있습니다.

| 문제 | 가능한 원인 | 가능한 솔루션 | |-|-|-| |Adobe으로 보낸 Roku SSO 헤더 없음|Adobe Primetime 인증 도메인 호출에 HTTPS 대신 HTTP를 사용|HTTPS 사용| |MVPD 로고가 표시되지 않음/SSO 토큰에 대해 업데이트되지 않음|UI는 로컬 저장소에 의존함|응용 프로그램은 인증을 확인한 후 UI(및 필요한 경우 로컬 저장소)를 업데이트해야 합니다.| |AuthZ에서 트리거된 로그아웃|응용 프로그램 디자인|백그라운드에서 로그아웃하지 않도록 응용 프로그램을 업데이트해야 합니다.|

## FAQ {#faq}

* **SSO는 어떻게 작동합니까?**

   SSO는 동일한 Roku 사용자와 연결된 모든 Roku 장치에서 Adobe Primetime 인증을 기반으로 하는 모든 Programmer 응용 프로그램에서 작동합니다.
일부 MVPD에서 Roku SSO를 허용하지 않습니다.

* **인증 TTL에 변경 사항이 있습니까?**

   첫 번째 유효한 인증 토큰은 SSO를 수행하는 데 사용되며, 이 경우 SSO를 통해 인증되는 다른 모든 응용 프로그램은 만료될 때까지 동일한 TTL을 사용합니다. 따라서 한 애플리케이션에서 다른 응용 프로그램으로 이동할 때 두 번째 응용 프로그램은 인증을 받는 첫 번째 응용 프로그램의 TTL을 공유합니다.

* **다른 Adobe 기능이 이전과 동일하게 작동합니까?**

   모든 Primetime 인증 기능은 이전과 동일하게 작동합니다.

* **Roku 플랫폼에서 SSO를 통해 혜택을 받는 프로그래머 옵트인/옵트아웃 프로세스가 있습니까?**

   Adobe의 TVE 대시보드에서 구성이 변경됩니다. 각 프로그래머는 특정 통합을 위해 Roku 플랫폼에서 SSO를 활성화/비활성화할 수 있습니다.
