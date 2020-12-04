---
description: Adobe Primetime DRM SDK에서 생성되는 모든 인증 토큰은 애플리케이션 보안을 보호하기 위해 시간 초과 간격이 있습니다.
seo-description: Adobe Primetime DRM SDK에서 생성되는 모든 인증 토큰은 애플리케이션 보안을 보호하기 위해 시간 초과 간격이 있습니다.
seo-title: 인증 토큰에 대한 시간 초과
title: 인증 토큰에 대한 시간 초과
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 인증 토큰 시간 초과{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK에서 생성되는 모든 인증 토큰은 애플리케이션 보안을 보호하기 위해 시간 초과 간격이 있습니다.

인증 요청을 처리할 때 인증 토큰 만료가 Primetime DRM SDK를 사용하십시오. 만료되면 토큰이 유효하지 않으므로 사용자가 라이선스 서버에 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)를 참조하십시오.
