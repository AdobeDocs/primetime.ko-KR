---
description: 라이선스는 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 기능을 허용 또는 거부할 수 있는 기본 메커니즘입니다. 합법적(권한 부여) 사용자는 라이센스(키)를 발급받아 컨텐츠 제공업체의 암호화된 특정 컨텐츠를 해독하고 재생할 수 있습니다.
seo-description: 라이선스는 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 기능을 허용 또는 거부할 수 있는 기본 메커니즘입니다. 합법적(권한 부여) 사용자는 라이센스(키)를 발급받아 컨텐츠 제공업체의 암호화된 특정 컨텐츠를 해독하고 재생할 수 있습니다.
seo-title: 라이선스
title: 라이선스
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 라이선스{#licensing}

라이선스는 사용자가 보호된 비디오 컨텐츠를 재생할 수 있는 기능을 허용 또는 거부할 수 있는 기본 메커니즘입니다. 합법적(권한 부여) 사용자는 라이센스(키)를 발급받아 컨텐츠 제공업체의 암호화된 특정 컨텐츠를 해독하고 재생할 수 있습니다.

최종 사용자의 장치에 있는 앱 또는 웹 페이지에서 DRM으로 보호된 콘텐츠를 재생하려면 먼저 고객이 운영하는 권한 부여 또는 스토어 프런트 서버에서 토큰을 확보해야 합니다. Adobe는 이러한 용도로 샘플 참조 서버를 제공합니다.참조 [서버:샘플 ExpressPlay 권한 부여 서버(SEE)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

권한 부여 또는 스토어 프런트 서버는 사용자의 백엔드 시스템을 통해 특정 사용자가 요청된 컨텐츠를 볼 수 있는지 여부를 확인한 후에만 관련 ExpressPlay Server에서 라이선스 토큰을 요청합니다. 라이선스 토큰 요청에서 반환되는 응답은 사용권 서버에 대해 바로 사용할 수 있는 URL이거나, 사용 중인 DRM 솔루션에 따라 JSON 구조의 URL을 응답에 포함합니다.

>[!NOTE]
>
>클라이언트 자체에서 라이선스 토큰 요청을 수행할 수 없습니다.
>1. 권한 부여는 신뢰할 수 있는 환경에서 확인해야 합니다.and
>1. 고객 인증자는 비밀로 유지해야 합니다.


1. 라이선스 토큰 요청

   관련된 다양한 구성 요소가 함께 작동되도록 하는 빠른 시작 시나리오의 경우, 라이선스 토큰 요청을 [!DNL curl] 위해(처음에 앱을 설치하여 실행하고 여기에서 테스트 호출을 가져오는 것과 반대)와 같은 기능을 사용할 수 있습니다. 예:

   * 위드바인:

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

   Widevine 응답은 &quot;즉시 사용&quot; URL 문자열입니다.

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

   PlayReady 응답은 별도의 URL 및 토큰 요소가 있는 JSON 개체입니다.

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

   FairPlay 응답은 &quot;즉시 사용&quot; URL 문자열입니다.
