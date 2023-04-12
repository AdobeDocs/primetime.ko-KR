---
title: Adobe Primetime 인증 2.64.1 릴리스 노트
description: Adobe Primetime 인증 2.64.1 릴리스 노트
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Adobe Primetime 인증 2.64.1 릴리스 노트 {#authn-264-rn}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

이 페이지에서는 이 릴리스의 새로운 기능, 변경 사항 및 알려진 문제에 대해 설명합니다.

## 서버 측 및 웹 클라이언트 {#server-side-web-clients-2641}

* [빌드 번호](#build-number-2641)
* [릴리스 개요](#release-overview-2641)

### 빌드 번호 {#build-number-2641}

Adobe Primetime 인증: adobe-pass-**2.64.1**
릴리스 날짜: **01/31/2023 - 02/02/2023**

### 릴리스 개요 {#release-overview-2641}

이 릴리스는 다음을 추가합니다.

* SAML 검증에 &quot;in_response_to&quot; 매개 변수가 없는 MVPD의 요청되지 않은 인증 응답을 차단하는 기능.
* 보안 요구 사항을 준수하기 위해 redirect_url 매개 변수에 대한 유효성 검사가 개선되었습니다.
* 초기 장치로부터 제공되는 정보를 이용하여 제2 화면 인증 요청을 위한 장치 정보 로깅을 개선한다.
