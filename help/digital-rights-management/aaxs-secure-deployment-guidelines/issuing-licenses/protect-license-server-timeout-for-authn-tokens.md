---
seo-title: 인증 토큰에 대한 시간 초과
title: 인증 토큰에 대한 시간 초과
uuid: 41b0fbf5-a567-4118-bec1-c05e6e0b6d1f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 인증 토큰 시간 초과{#timeout-for-authentication-tokens}

Adobe 액세스 SDK로 생성된 모든 인증 토큰은 애플리케이션 보안을 보호하기 위해 시간 초과 간격이 있습니다. 인증 토큰의 만료가 지정되면 인증 요청을 처리할 때 Adobe 액세스 SDK를 사용합니다. 만료가 지나면 인증 토큰이 더 이상 유효하지 않으므로 사용자가 라이선스 서버에 다시 인증해야 합니다.

인증 요청에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;의 AuthenticationHandler를 참조하십시오.
