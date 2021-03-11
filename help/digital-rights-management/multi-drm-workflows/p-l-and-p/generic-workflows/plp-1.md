---
description: ExpressPlay 기반의 Primetime Cloud DRM에서 지원하는 모든 DRM 솔루션에 대한 콘텐츠를 Adobe의 오프라인 패키저를 사용하여 준비할 수 있습니다.
title: Primetime Packager / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

ExpressPlay 기반의 Primetime Cloud DRM에서 지원하는 모든 DRM 솔루션에 대한 콘텐츠를 Adobe의 오프라인 패키저를 사용하여 준비할 수 있습니다.

이 지침에서는 ExpressPlay 관리자 계정을 이미 설정했다고 가정합니다.[Primetime DRM 클라우드 빠른 시작](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. 컨텐츠 패키징에 사용할 인프라를 선택하십시오. Primetime Packager는 FairPlay, Widevine 및 PlayReady DRM과 함께 사용할 수 있도록 명령줄 및 구성 기반의 콘텐츠 패키징을 지원합니다. 다음 형식 및 암호화는 현재 TVSDK에서 지원됩니다(파이프라인에 대한 자세한 내용).

   * DASH(CENC) / PlayReady, Widevine - HTML5용
   * HLS / FairPlay, Access - iOS용

1. 키 관리 시스템(KMS)을 선택합니다.

   * ExpressPlay의 KMS([ExpressPlay 키 저장소](https://www.expressplay.com/developer/key-storage/)) 사용;이 시스템은 ExpressPlay의 RESTful API를 통해 컨텐츠 키를 관리합니다.

      또는...

   * 고유한 KMS를 설정합니다. 콘텐츠 ID로 선택 가능한 콘텐츠 키 데이터베이스를 만듭니다.

      두 경우 모두 KMS에서 각 키에 연결된 Content-ID가 있는 콘텐츠 키 공급을 관리합니다.

1. 콘텐츠를 패키징합니다. Primetime Packager를 사용하면 특정 DRM 솔루션용 콘텐츠 또는 다양한 DRM 솔루션용 콘텐츠를 패키징할 수 있습니다.

   다음 샘플 명령은 다양한 DRM 솔루션에 대한 내용 패키징의 몇 가지 예를 보여줍니다.

   * [Primetime Packager가](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19)  있는 Widevine(MPD 파일 생성):

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [Primetime Packager를 사용한 FairPlay](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (M3U8 파일 생성):

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >`key_url` 값이 M3U8 파일에 있는 그대로 복사됩니다.

1. &quot;storefront 서버&quot;를 만듭니다.

       스토어 서버는 다음 작업을 처리해야 합니다.
   
   1. 고객이 선택한 컨텐츠 이 구현은 클라이언트가 특정 콘텐츠 ID에 대한 콘텐츠 토큰을 요청하는 끝점을 포함해야 합니다.
   1. 고객 자격 부여
   1. 클라이언트의 라이선스 토큰(ExpressPlay) 요청( [ExpressPlay 라이선스 토큰 요청 / 응답 참조](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. 클라이언트를 만듭니다.

       클라이언트는 스토어 서버 호출을 포함해야 합니다. Adobe은 사용자가 일부 콘텐트를 선택한 후, 사용자가 인증된 후에 클라이언트가 storefront를 호출하는 것이 좋습니다. 그런 다음 ExpressPlay에서 반환된 토큰을 플레이어로 전달하여 라이선스 요청에 사용합니다. 플레이어의 DRM 구성 요소 구현에 대한 소개:
   
   * [HTML5용 브라우저 TVSDK](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 현재 라이선스 토큰을 통해 클라이언트는 토큰에서 요청 URL을 추출하고 ExpressPlay에 라이선스 요청을 한 다음 사용자를 위해 선택한 컨텐츠를 재생할 수 있습니다.
