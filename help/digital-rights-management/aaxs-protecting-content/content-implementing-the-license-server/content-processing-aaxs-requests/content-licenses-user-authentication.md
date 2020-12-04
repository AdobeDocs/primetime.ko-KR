---
seo-title: 사용자 인증
title: 사용자 인증
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 사용자 인증{#user-authentication}

Adobe 액세스 요청에는 인증 토큰이 포함될 수 있습니다.

사용자 이름/암호 인증이 사용된 경우 요청에 `AuthenticationHandler`에서 생성된 `AuthenticationToken`이 포함될 수 있습니다. 토큰에 액세스하여 확인하려면 `RequestMessageBase.getAuthenticationToken()`을 사용하십시오. 클라이언트에서 사용자 이름/암호 요청을 시작하려면 `DRMManager.authenticate()` ActionScript 또는 iOS API를 사용하십시오.

클라이언트와 서버가 사용자 정의 인증 메커니즘을 사용하는 경우 클라이언트는 다른 채널을 통해 인증 토큰을 입수하고 `DRMManager.setAuthenticationToken` ActionScript 3.0 API를 사용하여 사용자 정의 인증 토큰을 설정합니다. `RequestMessageBase.getRawAuthenticationToken()`을(를) 사용하여 사용자 정의 인증 토큰을 가져옵니다. 서버 구현은 사용자 지정 인증 토큰이 유효한지 여부를 결정할 책임이 있습니다.
