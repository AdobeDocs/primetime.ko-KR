---
title: 익명 도메인 등록 구현
description: 익명 도메인 등록 구현
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 익명 도메인 등록 구현{#implement-anonymous-domain-registration}

1. 도메인 등록이 필수임을 지정하는 DRM 정책을 만듭니다.
1. 도메인 서버 URL을 다음과 같이 지정합니다.

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 익명 인증을 의무화하십시오.

   [!DNL .properties] 파일에서 다음을 설정합니다.

   ```
   policy.domain.anonymous=true 
   ```
