---
description: TVSDK 앱에서 FairPlay 스트리밍을 구현하려면 리소스 로더를 작성해야 하며, 이 로더는 FairPlay 스트리밍 서버에 라이선스 획득 요청을 보냅니다.
title: TVSDK 애플리케이션의 Apple FairPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# TVSDK 애플리케이션의 Apple FairPlay  {#apple-fairplay-in-tvsdk-applications}

TVSDK 앱에서 FairPlay 스트리밍을 구현하려면 리소스 로더를 작성해야 하며, 이 로더는 FairPlay 스트리밍 서버에 라이선스 획득 요청을 보냅니다.

리소스 로더 코드는 다음 작업을 담당합니다.

1. 라이선스 획득 요청을 보낼 위치를 결정합니다.
1. 요청 형식을 지정합니다.
1. 서버에서 요청을 허용할지 여부를 결정할 수 있도록 서버에 필요한 정보를 제공합니다.

예를 들어 ExpressPlay에서 제공하는 Adobe의 Primetime Cloud DRM을 사용하는 경우 리소스 로더가 요청을 다음으로 보냅니다.

```
https://fp-gen.service.expressplay.com
```

리소스 로더는 요청 형식을 지정하고 재생을 승인하는 ExpressPlay 토큰을 URL에 첨부합니다. ExpressPlay 토큰을 가져올 때 고려해야 할 몇 가지 옵션이 있습니다. 이러한 옵션은 콘텐츠를 패키지한 방법에 따라 결정됩니다.

콘텐츠를 패키지할 때 패키지 작성자는 를 삽입합니다 `skd:` M3U8 매니페스트의 URL. 다음 이후 `skd:` 항목을 입력하면 매니페스트에 모든 데이터를 넣을 수 있습니다. 애플리케이션 코드에서 이 데이터를 사용하여 위에 나열된 작업을 완료할 수 있습니다. 예를 들어 다음을 사용할 수 있습니다. `skd:{content_id}` 따라서 앱이 재생 중인 콘텐츠의 ID를 결정하고 해당 특정 콘텐츠에 대한 토큰을 요청할 수 있습니다. 예를 들어 다음을 사용할 수도 있습니다 `skd:{entitlement_server_url}?cid={content_id}`따라서 앱에 권한 부여 서버 URL이 하드코딩될 필요가 없습니다.

에 정보가 필요하지 않을 수 있습니다. `skd:` 재생이 시작될 때 다른 채널을 통해 콘텐츠 ID를 이미 알고 있는 경우 URL입니다. 두 번째 예는 설정을 테스트하는 데 이상적인 솔루션이지만 프로덕션 환경에서도 사용할 수 있습니다.

>[!TIP]
>
>형식을 결정합니다. `skd:`.

콘텐츠는 다음을 사용하여 가져옵니다. `skd:` 프로토콜을 사용하지만 라이선스 요청에서는 `https:`. 이러한 프로토콜을 처리하는 가장 일반적인 옵션은 다음과 같습니다.

* **엔드 투 엔드 재생 초기 테스트** 콘텐츠를 패키징할 때 `skd:` URL. 앱을 테스트할 때 ExpressPlay에서 라이선스를 수동으로 획득하고 라이선스를 하드코드(및 `https:` URL)과 콘텐츠 URL이 들어 있습니다.

  예:

  ```
  NSString* const PLAYLIST_URL =  
    @"https://{your_content_URL}/{your_manifest}.m3u8"; 
  NSString* const EXPRESSPLAY_TOKEN =  
    @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
      ExpressPlayToken={copy_your_token_to_here}";
  ```

* **대부분의 기타 사례** 콘텐츠를 패키징할 때 `skd:` 콘텐츠의 ID를 고유하게 나타내는 URL입니다. 로더에서 `skd:` URL을 만든 후 서버에 보내어 토큰을 얻은 다음 결과 토큰을 URL로 사용합니다.

  예:

  ```
  - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
        shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
      NSURL *url = [[loadingRequest request] URL]; 
      if (![[url scheme] isEqual:@"skd"]) 
          return NO; 
  
      NSString *strUrl = [url absoluteString]; 
      NSLog(@"url is: %@", strUrl); 
  
      strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
  
      NSData *assetId; 
  
      NSData *requestBytes; 
      NSError* error = nil; 
      BOOL handled = NO; 
  
      NSData  *responseData = nil; 
  
      assetId = getMyAssetIdentifierFromURL(url); 
  
      /* Usecase 1: "On Premise Fairplay Server" 
       * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
       * Server Url is either hardcoded in the App or derived from strUrl. 
       */ 
  #if 0  
      // Insert your use case 1 codes here: 
      // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
  #endif // 
  
      /* Usecase 2: The strUrl is the entitlement server. 
       * Send assetId to the entitlement server; if the user is allowed to playback  
       * the content, the entitlement server will send back an ExpressPlay Token Url. 
       */ 
  
  #if 0 
      // The hardcoded SEES server: 
      strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
  
      // You can use the following code to simulate a device binding entitlement  
      // request:  
      // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
      // bEnforceDeviceID set to false. When you play the content, the device_id  
      // will be registered on the ExpressPlay Server.  Now change code to set  
      // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
      // sent back by the SEES server will be device bound. 
  
      // The strUrl returned below is the ExpressPlay Token URL. 
      strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
  #endif 
  
      /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
       */ 
  
      // Read in the certificate 
      NSLog(@"Get Application Certificate"); 
      NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                           ofType:nil]; 
  
      NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
  
      // To create the request blob for the server: 
      requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                        contentIdentifier:assetId  
                                                                  options:nil  
                                                                    error:&error]; 
      if (requestBytes == nil) { 
          NSLog(@"Error creating server request: %@", error); 
          return false; 
      } 
      // Per the specification, send requestBytes along with the assetId to the Key 
      // Server and obtain the response. 
      NSError *err; 
  
      responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
  
      if (responseData != nil) { 
          NSLog(@"Get response data: "); 
          [loadingRequest finishLoadingWithResponse:nil  
                                               data:(NSData *)responseData 
                                           redirect:nil]; 
      } 
      else { 
          [loadingRequest finishLoadingWithError:err]; 
          NSLog(@"bad key response"); 
      } 
      handled = YES; 
  bail: 
      return handled; 
  
  }
  ```

## TVSDK 애플리케이션에서 Apple FairPlay 활성화{#enable-apple-fairplay-in-tvsdk-applications}

Apple의 DRM 솔루션인 Apple FairPlay 스트리밍을 TVSDK 애플리케이션에서 구현할 수 있습니다.

1. 다음을 구현하여 FairPlay 고객 리소스 로더 만들기 `PTAVAssetResourceLoaderDelegate`.

   자세한 내용은 [TVSDK 애플리케이션의 Apple FairPlay](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

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
