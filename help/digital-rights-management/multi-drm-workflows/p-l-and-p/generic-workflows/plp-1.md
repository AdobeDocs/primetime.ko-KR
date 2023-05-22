---
description: Adobe의 Offline packager를 사용하여 ExpressPlay에서 제공하는 Primetime Cloud DRM에서 지원하는 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.
title: Primetime Packager / Cloud DRM / TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Adobe의 Offline packager를 사용하여 ExpressPlay에서 제공하는 Primetime Cloud DRM에서 지원하는 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.

이 일련의 지침은 ExpressPlay 관리자 계정을 이미 설정했다고 가정합니다. [Primetime DRM 클라우드 빠른 시작](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. 콘텐츠를 패키지화하는 데 사용할 인프라를 선택합니다. Primetime Packager는 FairPlay, Widevine 및 PlayReady DRM과 함께 사용할 수 있는 컨텐츠의 명령줄 및 구성 기반 패키징을 모두 지원합니다. 다음 형식 및 암호화는 현재 TVSDK에서 지원됩니다(파이프라인에 더 많은 내용이 포함됨).

   * DASH (CENC) / PlayReady, Widevine - HTML 5용
   * HLS / FairPlay, 액세스 - iOS

1. KMS(키 관리 시스템) 선택:

   * ExpressPlay의 KMS 사용( [ExpressPlay 키 저장소](https://www.expressplay.com/developer/key-storage/)); 이 시스템은 ExpressPlay의 RESTful API를 통해 콘텐츠 키를 관리합니다.

      또는...

   * 자체 KMS를 설정합니다. Content-ID로 선택할 수 있는 콘텐츠 키 데이터베이스를 만듭니다.

      어느 경우든지, KMS는 각 키가 연관된 Content-ID를 가지는 콘텐츠 키의 공급을 관리한다.

1. 콘텐츠를 패키징합니다. Primetime Packager를 사용하면 특정 DRM 솔루션 또는 여러 DRM 솔루션에 대한 콘텐츠를 패키징할 수 있습니다.

   다음 샘플 명령은 서로 다른 DRM 솔루션에 대한 콘텐츠를 패키지하는 몇 가지 예를 보여 줍니다.

   * [Widevine with Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) (MPD 파일 생성):

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

   * [Primetime Packager와 함께 FairPlay](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (M3U8 파일 생성):

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
      >다음 `key_url` 값은 M3U8 파일에 있는 그대로 복사됩니다.

1. &quot;storefront 서버&quot;를 만듭니다.

       Storefront 서버는 다음 작업을 처리해야 합니다.
   
   1. 고객이 콘텐츠를 선택합니다. 이 구현에는 클라이언트가 특정 콘텐츠 ID에 대한 콘텐츠 토큰을 요청할 수 있는 엔드포인트가 포함되어야 합니다.
   1. 고객 권한
   1. 클라이언트의 라이센스 토큰(ExpressPlay) 요청( [ExpressPlay 라이선스 토큰 요청/응답 참조](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. 클라이언트를 만듭니다.

       클라이언트에는 Storefront 서버에 대한 호출이 포함되어야 합니다. Adobe은 사용자가 일부 콘텐츠를 선택한 후, 사용자가 인증된 후에 클라이언트가 상점 첫 페이지를 호출하는 것을 권장합니다. 그런 다음 ExpressPlay에서 반환된 토큰을 플레이어에 전달하여 라이센스 요청에 사용합니다. 플레이어의 DRM 구성 요소 구현에 대한 소개는 다음과 같습니다.
   
   * [HTML 5용 브라우저 TVSDK](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 이제 라이선스 토큰을 사용하여 클라이언트는 토큰에서 요청 URL을 파생하고 ExpressPlay에 라이선스 요청을 한 다음 사용자에 대해 선택한 콘텐츠를 재생할 수 있습니다.
