---
seo-title: 익명 도메인 등록 구현
title: 익명 도메인 등록 구현
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 익명 도메인 등록 구현{#implement-anonymous-domain-registration}

1. 도메인 등록이 필요함을 지정하는 DRM 정책을 만듭니다.
1. 도메인 서버 URL을 다음과 같이 지정합니다.

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 익명 인증을 의무화하십시오.

   [!DNL .properties] 파일에서 다음을 설정합니다.

   ```
   policy.domain.anonymous=true 
   ```
