---
description: Adobe Primetime DRM SDK에서 생성한 모든 인증 토큰에는 애플리케이션 보안을 보호하기 위한 시간 제한 간격이 있습니다.
title: 인증 토큰 시간 제한
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 인증 토큰 시간 제한{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK에서 생성한 모든 인증 토큰에는 애플리케이션 보안을 보호하기 위한 시간 제한 간격이 있습니다.

인증 토큰에 대한 만료는 인증 요청을 처리할 때 Primetime DRM SDK를 사용하여 지정합니다. 토큰이 만료되면 더 이상 유효하지 않으므로 사용자는 라이선스 서버를 사용하여 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 다음을 참조하십시오. [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
