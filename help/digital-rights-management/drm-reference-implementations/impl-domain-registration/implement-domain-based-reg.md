---
title: ID 기반 도메인 등록 구현
description: ID 기반 도메인 등록 구현
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# ID 기반 도메인 등록 구현{#implement-identity-based-domain-registration}

1. 필수 도메인 등록으로 DRM 정책을 만듭니다.
1. 도메인 서버 URL에 대한 서버의 호스트 및 포트를 지정합니다.

   [!DNL .properties] 파일에서 다음을 설정합니다.

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 사용자 이름과 암호를 사용하여 인증을 필수 항목으로 지정합니다.

   [!DNL .properties] 파일에서 다음을 설정합니다.

   ```
   policy.domain.anonymous=false 
   ```
