---
title: Clientless API 구현 - 가능한 이유/원인이 있는 오류 코드/메시지
description: Clientless API 구현 - 가능한 이유/원인이 있는 오류 코드/메시지
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Clientless API 구현 - 가능한 이유/원인이 있는 오류 코드/메시지 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

</br>


## 오류: 승인되지 않음

### 원인:

1. POST에 인증 헤더 누락
1. 인증 헤더 문제 - 요청 시간이 밀리초 단위인지 확인하십시오.

## 오류: 인증하는 동안 SC 400

### 원인:

1. 서버가 특정 요청자 및 환경에 대해 만들어진 등록 코드를 찾지 못했습니다.
1. 도메인 간 스크립팅 문제가 발생할 수 있습니다
1. /etc/hosts 파일에 적절한 스푸핑을 추가해야 합니다.

## 오류: 400개의 잘못된 요청

### 원인:

1. POST/GET에 대한 잘못된 URL
1. SAMLAssertionParserException - Adobe 끝에서 암호화된 SAML 어설션의 암호를 해독할 수 없습니다.

## 오류: 403 금지됨

### 원인:

1. 너무 많은 빠른 요청 - DoS 공격을 방지하기 위한 API 관리 기능입니다.
2. 프리컬 환경을 사용하는 경우 스푸핑을 추가하고 그렇지 않으면 /etc/hosts 파일에서 스푸핑이 제거되었는지 확인합니다

## 오류: MVPD 페이지에 로그인할 수 없습니다.

### 원인:

1. 사용자 이름과 암호가 일치하지 않습니다. 
2. 로그인이 비활성화되었을 수 있습니다.
3. 로그인이 프로덕션 또는 스테이징용인지 확인


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
