---
seo-title: 사용자 인증
title: 사용자 인증
uuid: 5cbd76b9-ff64-4a4b-8cfd-54f05c04eaa3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 사용자 인증 {#user-authentication}

Adobe Primetime DRM 요청에는 인증 토큰이 포함될 수 있습니다.

사용자 이름/암호 인증이 사용된 경우, 요청에는 에서 `AuthenticationToken` 생성된 ID가 포함될 수 `AuthenticationHandler`있습니다. 토큰에 액세스하여 확인하려면 반드시 사용해야 합니다 `RequestMessageBase.getAuthenticationToken()`. 클라이언트에서 사용자 이름/암호 요청을 시작하려면 ActionScript 또는 iOS API를 `DRMManager.authenticate()` 사용합니다.

클라이언트와 서버가 사용자 정의 인증 메커니즘을 사용하는 경우 클라이언트는 다른 채널을 통해 인증 토큰을 입수하고 ActionScript 3.0 API를 사용하여 사용자 정의 인증 토큰을 `DRMManager.setAuthenticationToken` 설정합니다. 사용자 정의 인증 토큰을 `RequestMessageBase.getRawAuthenticationToken()` 가져오는 데 사용합니다. 서버 구현은 사용자 정의 인증 토큰이 유효한지 여부를 결정합니다.
