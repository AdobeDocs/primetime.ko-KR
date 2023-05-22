---
title: ID 기반 도메인 등록 구현
description: ID 기반 도메인 등록 구현
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# ID 기반 도메인 등록 구현{#implement-identity-based-domain-registration}

1. 필수 도메인 등록을 사용하여 DRM 정책을 만듭니다.
1. 도메인 서버 URL에 대한 서버의 호스트 및 포트를 지정합니다.

   내 [!DNL .properties] 파일, 설정:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 사용자 이름과 암호를 사용한 인증은 필수입니다.

   내 [!DNL .properties] 파일, 설정:

   ```
   policy.domain.anonymous=false 
   ```
