---
description: TVSDK 애플리케이션에서 Apple의 DRM 솔루션인 Apple FairPlay Streaming을 구현할 수 있습니다.
seo-description: TVSDK 애플리케이션에서 Apple의 DRM 솔루션인 Apple FairPlay Streaming을 구현할 수 있습니다.
seo-title: TVSDK 애플리케이션에서 Apple FairPlay 사용
title: TVSDK 애플리케이션에서 Apple FairPlay 사용
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# TVSDK 애플리케이션에서 Apple FairPlay 사용{#enable-apple-fairplay-in-tvsdk-applications}

TVSDK 애플리케이션에서 Apple의 DRM 솔루션인 Apple FairPlay Streaming을 구현할 수 있습니다.

1. `PTAVAssetResourceLoaderDelegate`을(를) 구현하여 FairPlay 고객 리소스 로더를 만듭니다.

   자세한 내용은 [TVSDK 응용 프로그램의 Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)를 참조하십시오.

   >[!NOTE]
   >
   >[FPS 인식 앱 개발을 위한 FairPlay Server SDK](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)에 포함되어 있는 *FairPlay 스트리밍 프로그램 안내서*(*FairPlayStreaming_PG.pdf*)의 지침을 따라야 합니다.

   `resourceLoader:shouldWaitForLoadingOfRequestedResource` 메서드는 `AVAssetResourceLoaderDelegate`에 있는 메서드에 해당합니다.

   >[!IMPORTANT]
   >
   >ExpressPlay 라이선스 서버 시나리오에서 콘텐트를 재생하려면 ExpressPlay FairPlay 서버 라이선스 요청 URL의 URL 체계를 `skd://`에서 `https://`(또는 `https://`)으로 변경하십시오.

1. *FairPlay* 고객 리소스 로더를 `registerPTAVAssetResourceLoader`와(와) 등록하십시오.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

FairPlay 라이선스 서버를 직접 작성하거나 타사 FairPlay 라이선스 서버를 사용하는 경우 라이선스 서버 공급업체에 문의하여 라이선스 서버 URL, 서식 및 기타 요구 사항을 확인하십시오.
