---
title: 인증 토큰에 대한 시간 초과
description: 인증 토큰에 대한 시간 초과
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 인증 토큰 시간 초과{#timeout-for-authentication-tokens}

Adobe 액세스 SDK로 생성된 모든 인증 토큰에는 응용 프로그램 보안을 보호하기 위한 시간 초과 간격이 있습니다. 인증 토큰의 만료가 지정되면 인증 요청을 처리할 때 Adobe 액세스 SDK를 사용합니다. 만료가 지나면 인증 토큰이 더 이상 유효하지 않으므로 사용자가 라이선스 서버에 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;의 AuthenticationHandler를 참조하십시오.
