---
title: Adobe Primetime 인증 2.64 릴리스 노트
description: Adobe Primetime 인증 2.64 릴리스 노트
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Adobe Primetime 인증 2.64 릴리스 노트 {#authn-264-rn}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

이 페이지에서는 이 릴리스의 새로운 기능, 변경 사항 및 알려진 문제에 대해 설명합니다.

## 서버 측 및 웹 클라이언트 {#ss-web-clients}

* [빌드 번호](#build-no-264)
* [새로운 기능](#new-featres-264)
* [버그 수정](#bug-fixes-264)


### 빌드 번호 {#build-no-264}

Adobe Primetime 인증: adobe-pass-**2.64**

릴리스 날짜: **11/08/2022 - 11/10/2022**

### 새로운 기능 {#new-featres-264}

* 서버 응답 시간을 줄여 전체 시스템 성능을 향상시키는 인프라 업데이트
* 새로운 플랫폼 식별 메커니즘이 개선되었습니다.
* SAML 어설션에서 &quot;in_response_to&quot; 매개 변수가 누락된 MVPD의 요청되지 않은 인증 응답을 차단하는 기능.

### 버그 수정 {#bug-fixes-264}

* 일부 기존 TempPass 토큰의 잘못된 형식을 수정했습니다.
* 두 번째 화면 인증 흐름에서 사소한 문제가 해결되었습니다.
