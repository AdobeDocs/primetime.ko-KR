---
title: 익명 도메인 등록 구현
description: 익명 도메인 등록 구현
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
