---
title: Clientless API 구현-오류 코드/메시지가 예상 원인/원인
description: Clientless API 구현-오류 코드/메시지가 예상 원인/원인
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Clientless API 구현-오류 코드/메시지가 예상 원인/원인 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>이 페이지의 컨텐츠은 정보 제공 목적 으로만 제공 됩니다. 이 API를 사용 하려면 Adobe Systems에서 현재 라이센스가 필요 합니다. 허가되지 않은 사용은 허용되지 않습니다.

</br>


## 오류: 인증 되지 않음

### 원인:

1. POST에 인증 헤더가 없습니다.
1. 인증 헤더 관련 문제-요청 시간이 밀리초 단위 인지 확인 합니다.

## 오류: 인증 중 SC 400

### 원인:

1. 서버가 특정 요청자 및 환경용으로 작성 된 등록 코드를 찾지 못했습니다.
1. 도메인 간 스크립팅 문제를 실행할 수 있습니다.
1. 적절 한 스푸핑을/etc/hosts 파일에 추가 해야 합니다.

## 오류: 400 잘못 된 요청

### 원인:

1. POST/GET의 잘못 된 url
1. SAMLAssertionParserException – 암호화 된 SAML 어설션을 Adobe Systems의 끝에서 해독할 수 없습니다.

## 오류: 403 금지 됨

### 원인:

1. DoS 공격을 방지 하는 API 관리 기능을 통해 너무 많은 빠른 요청을 했습니다.
2. Prequal 환경을 사용 하는 경우 스푸핑을 추가 합니다. 그렇지 않으면/etc/hosts 파일에서 스푸핑이 제거 되었는지 확인 하십시오.

## 오류: MVPD에 로그인 할 수 없습니다 페이지

### 원인:

1. 사용자 이름 및 암호 일치 하지 않음
2. 로그인이 비활성화 되었을 수 있습니다.
3. 로그인이 프로덕션 또는 스테이징용인지 확인


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
