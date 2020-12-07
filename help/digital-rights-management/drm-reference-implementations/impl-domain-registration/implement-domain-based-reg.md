---
seo-title: ID 기반 도메인 등록 구현
title: ID 기반 도메인 등록 구현
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
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
