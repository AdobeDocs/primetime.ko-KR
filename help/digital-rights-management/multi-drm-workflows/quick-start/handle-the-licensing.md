---
description: 라이선스는 사용자가 보호된 비디오 컨텐츠를 재생하는 기능을 허용 또는 거부할 수 있는 기본 메커니즘입니다. 합법적(권한 부여) 사용자는 해당 컨텐트 공급자의 암호화된 컨텐츠의 특정 부분을 해독하고 재생하기 위한 라이센스(키)를 발급받을 수 있습니다.
title: 라이선스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# 라이선스{#licensing}

라이선스는 사용자가 보호된 비디오 컨텐츠를 재생하는 기능을 허용 또는 거부할 수 있는 기본 메커니즘입니다. 합법적(권한 부여) 사용자는 해당 컨텐트 공급자의 암호화된 컨텐츠의 특정 부분을 해독하고 재생하기 위한 라이센스(키)를 발급받을 수 있습니다.

최종 사용자의 장치에 있는 앱 또는 웹 페이지에서 DRM으로 보호된 콘텐츠를 재생하기 전에 고객이 운영하는 권한 부여 또는 스토어 프런트 서버에서 토큰을 확보해야 합니다. Adobe은 이러한 목적으로 샘플 참조 서버를 제공합니다.[참조 서버:샘플 ExpressPlay 자격 부여 서버(SEE)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

권한 부여 또는 스토어 프런트 서버는 특정 사용자가 요청된 컨텐츠를 볼 수 있는 권한이 있는지 확인하기 위해 자체 백엔드 시스템을 확인한 후 관련 ExpressPlay Server에서 라이선스 토큰을 요청합니다. 라이선스 토큰 요청에서 반환되는 응답은 라이선스 서버에 즉시 사용할 수 있는 URL이거나 응답에 작업 중인 DRM 솔루션에 따라 JSON 구조의 URL이 포함됩니다.

>[!NOTE]
>
>클라이언트 자체에서 라이선스 토큰 요청을 수행할 수 없습니다.
>1. 신뢰할 수 있는 환경에서 권한을 확인해야 합니다.and
>1. 고객 인증자는 비밀로 유지해야 합니다.


1. 라이센스 토큰 요청을 수행합니다.

   관련된 다양한 구성 요소가 서로 연동되도록 하는 빠른 시작 시나리오의 경우, [!DNL curl]과 같은 기능을 사용하여 라이선스 토큰 요청을 할 수 있습니다(처음에 앱을 시작하고 실행하며 여기에서 호출을 테스트하는 것과는 반대). 예:

   * 무선:

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

   샘플 무선 테스트 토큰:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   무선 응답은 &quot;즉시 사용할 수 있는&quot; URL 문자열입니다.

   * PlayReady:

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

   PlayReady 응답은 별도의 URL 및 토큰 요소가 포함된 JSON 개체입니다.

   * FairPlay:

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

   FairPlay 응답은 &quot;바로 사용할 수 있는&quot; URL 문자열입니다.
