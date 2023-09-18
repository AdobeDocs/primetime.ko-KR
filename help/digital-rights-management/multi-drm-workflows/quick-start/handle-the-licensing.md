---
description: 라이선스는 사용자가 보호된 비디오 콘텐츠의 일부를 재생하는 기능을 허용하거나 거부하는 기본 메커니즘입니다. 합법적인(권한이 있는) 사용자는 콘텐츠 공급자의 암호화된 콘텐츠의 특정 부분을 해독하고 재생할 수 있는 라이선스(키)를 발급받을 수 있습니다.
title: 라이선스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 라이선스{#licensing}

라이선스는 사용자가 보호된 비디오 콘텐츠의 일부를 재생하는 기능을 허용하거나 거부하는 기본 메커니즘입니다. 합법적인(권한이 있는) 사용자는 콘텐츠 공급자의 암호화된 콘텐츠의 특정 부분을 해독하고 재생할 수 있는 라이선스(키)를 발급받을 수 있습니다.

최종 사용자의 장치에서 앱 또는 웹 페이지가 DRM으로 보호된 콘텐츠를 재생하려면 먼저 고객이 운영하는 권한 또는 상점 서버에서 토큰을 얻어야 합니다. Adobe은 이러한 목적을 위한 샘플 참조 서버를 제공합니다. [참조 서버: 샘플 ExpressPlay 권한 서버(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

특정 사용자가 요청된 콘텐츠를 시청할 자격이 있는지 여부를 자체 백엔드 시스템에 확인한 후에만 자격 부여 또는 상점 서버가 해당 ExpressPlay 서버에 라이선스 토큰을 요청합니다. 라이센스 토큰 요청에서 반환된 응답은 작업 중인 DRM 솔루션에 따라 라이센스 서버의 사용 준비 URL이거나 응답에 JSON 구조의 URL이 포함되어 있습니다.

>[!NOTE]
>
>클라이언트 자체에서 라이선스 토큰 요청을 수행할 수 없습니다.
>1. 신뢰할 수 있는 환경에서 권한을 확인해야 합니다.
>1. 고객 인증자는 비밀로 유지되어야 합니다.

1. 라이선스 토큰 요청을 만듭니다.

   관련된 다양한 구성 요소가 함께 작동하는지 확인하고자 하는 빠른 시작 시나리오에서는 다음과 같은 항목을 사용할 수 있습니다 [!DNL curl] (처음에 앱을 시작하고 실행하며 이 앱에서 호출을 테스트하는 것과 대조적으로) 라이선스 토큰 요청을 수행하려면 다음을 수행합니다. 예:

   * Widevine:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   샘플 와이드빈 테스트 토큰:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Widevine 응답은 &quot;사용 준비&quot; URL 문자열입니다.

   * 재생 준비:

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   샘플 PlayReady 테스트 토큰:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   PlayReady 응답은 별도의 URL 및 토큰 요소가 있는 JSON 개체입니다.

   * 페어플레이:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   샘플 FairPlay 테스트 토큰:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   FairPlay 응답은 &quot;사용 준비&quot; URL 문자열입니다.
