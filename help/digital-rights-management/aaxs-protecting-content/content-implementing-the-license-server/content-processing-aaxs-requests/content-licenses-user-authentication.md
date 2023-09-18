---
title: 사용자 인증
description: 사용자 인증
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 사용자 인증{#user-authentication}

Adobe 액세스 요청에는 인증 토큰이 포함될 수 있습니다.

사용자 이름/암호 인증을 사용한 경우 요청에 `AuthenticationToken` 생성된 사람 `AuthenticationHandler`. 토큰에 액세스하고 확인하려면 `RequestMessageBase.getAuthenticationToken()`. 클라이언트에서 사용자 이름/암호 요청을 시작하려면 `DRMManager.authenticate()` ActionScript 또는 iOS API입니다.

클라이언트와 서버가 사용자 지정 인증 메커니즘을 사용하는 경우 클라이언트는 다른 채널을 통해 인증 토큰을 획득하고 다음을 사용하여 사용자 지정 인증 토큰을 설정합니다. `DRMManager.setAuthenticationToken` ActionScript 3.0 API입니다. 사용 `RequestMessageBase.getRawAuthenticationToken()` 사용자 지정 인증 토큰을 가져옵니다. 서버 구현은 사용자 지정 인증 토큰이 유효한지 여부를 결정합니다.
