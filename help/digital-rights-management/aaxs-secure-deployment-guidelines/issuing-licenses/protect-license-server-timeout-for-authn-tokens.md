---
title: 인증 토큰 시간 제한
description: 인증 토큰 시간 제한
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 인증 토큰 시간 제한{#timeout-for-authentication-tokens}

Adobe 액세스 SDK에서 생성한 모든 인증 토큰에는 애플리케이션 보안을 보호하기 위한 시간 제한 간격이 있습니다. 인증 토큰에 대한 만료가 지정되었으므로 인증 요청을 처리할 때 Adobe 액세스 SDK를 사용하십시오. 만료가 경과하면 인증 토큰이 더 이상 유효하지 않으므로 사용자는 라이선스 서버를 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 *Adobe 액세스 API 참조*.
