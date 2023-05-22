---
description: Apple의 DRM 솔루션인 Apple FairPlay 스트리밍을 TVSDK 애플리케이션에서 구현할 수 있습니다.
title: TVSDK 애플리케이션에서 Apple FairPlay 활성화
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# TVSDK 애플리케이션에서 Apple FairPlay 활성화{#enable-apple-fairplay-in-tvsdk-applications}

Apple의 DRM 솔루션인 Apple FairPlay 스트리밍을 TVSDK 애플리케이션에서 구현할 수 있습니다.

1. 다음을 구현하여 FairPlay 고객 리소스 로더 만들기 `PTAVAssetResourceLoaderDelegate`.

   자세한 내용은 [TVSDK 애플리케이션의 Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >의 지침을 따르는지 확인합니다. *FairPlay 스트리밍 프로그램 안내서* ( *FairPlayStreaming_PG.pdf*), 포함 [FPS 인식 앱 개발을 위한 FairPlay Server SDK](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   다음 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 메서드는 의 메서드와 동일합니다. `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >ExpressPlay 라이선스 서버 시나리오에서 콘텐츠를 재생하려면 ExpressPlay FairPlay 서버 라이선스 요청 URL에서 URL 체계를 변경합니다. `skd://` 끝 `https://` (또는 `https://`).

1. 등록 *페어플레이* 다음을 포함한 고객 리소스 로더 `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

FairPlay 라이선스 서버를 직접 작성했거나 타사 FairPlay 라이선스 서버를 사용하는 경우 라이선스 서버 공급업체에 문의하여 라이선스 서버 URL, 서식 및 기타 요구 사항을 확인하십시오.
