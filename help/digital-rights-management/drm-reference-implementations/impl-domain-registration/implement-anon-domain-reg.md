---
title: 익명 도메인 등록 구현
description: 익명 도메인 등록 구현
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 익명 도메인 등록 구현{#implement-anonymous-domain-registration}

1. 도메인 등록이 필요하도록 지정하는 DRM 정책을 생성합니다.
1. 도메인 서버 URL을 다음과 같이 지정합니다.

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 익명 인증을 필수로 설정합니다.

   내 [!DNL .properties] 파일, 설정:

   ```
   policy.domain.anonymous=true 
   ```
