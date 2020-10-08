---
description: TVSDK 앱에서 FairPlay 스트리밍을 구현하려면 Resource Loader를 작성하여 FairPlay 스트리밍 서버에 라이선스 획득 요청을 보내야 합니다.
seo-description: TVSDK 앱에서 FairPlay 스트리밍을 구현하려면 Resource Loader를 작성하여 FairPlay 스트리밍 서버에 라이선스 획득 요청을 보내야 합니다.
seo-title: TVSDK 애플리케이션의 Apple FairPlay
title: TVSDK 애플리케이션의 Apple FairPlay
uuid: 5796d5af-0018-4c69-a755-65e4819ee838
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# TVSDK 애플리케이션의 Apple FairPlay {#apple-fairplay-in-tvsdk-applications}

TVSDK 앱에서 FairPlay 스트리밍을 구현하려면 Resource Loader를 작성하여 FairPlay 스트리밍 서버에 라이선스 획득 요청을 보내야 합니다.

리소스 로더 코드는 다음 작업을 수행합니다.

1. 라이센스 획득 요청을 보낼 위치를 결정합니다.
1. 요청의 형식을 지정합니다.
1. 서버가 요청을 허용할지 여부를 결정할 수 있도록 필요한 정보를 서버에 제공하십시오.

예를 들어 ExpressPlay에서 제공하는 Adobe의 Primetime Cloud DRM을 사용하는 경우 Resource Loader가 다음을 통해 요청을 전송합니다.

```
https://fp-gen.service.expressplay.com
```

리소스 로더는 요청을 포맷하고 URL에 재생을 승인하는 ExpressPlay 토큰을 첨부합니다. ExpressPlay 토큰을 가져올 때 고려해야 할 몇 가지 옵션이 있습니다. 이러한 옵션은 컨텐츠를 패키지한 방법에 따라 결정됩니다.

컨텐츠를 패키지하면 Packager가 M3U8 매니페스트에 `skd:` URL을 삽입합니다. 항목이 `skd:` 끝나면 매니페스트에 데이터를 넣을 수 있습니다. 애플리케이션 코드에서 이 데이터를 사용하여 위에 나열된 작업을 완료할 수 있습니다. 예를 들어, 앱이 재생되는 콘텐츠의 ID를 확인하고 해당 특정 콘텐츠에 대한 토큰을 요청할 수 `skd:{content_id}` 있도록 사용할 수 있습니다. 예를 들어, 앱에서 권한 부여 서버 URL `skd:{entitlement_server_url}?cid={content_id}`을 하드 코딩하지 않아도 되도록 사용할 수도 있습니다.

재생이 시작될 때 다른 채널을 통해 이미 컨텐츠 ID를 알고 있는 경우 `skd:` URL에 어떤 정보도 필요하지 않을 수 있습니다. 두 번째 예는 설정을 테스트하는 데 이상적인 솔루션이지만 프로덕션 환경에서도 사용할 수 있습니다.

>[!TIP]
>
>형식을 결정합니다 `skd:`.

귀하의 컨텐트는 `skd:` 프로토콜을 사용하여 얻지만 라이센스 요청은 이를 사용합니다 `https:`. 이러한 프로토콜을 처리하기 위한 가장 일반적인 옵션은 다음과 같습니다.

* **엔드 투 엔드 재생** 초기 테스트 컨텐츠를 패키지화할 때 `skd:` URL을 선택합니다. 앱을 테스트할 때 ExpressPlay에서 라이선스를 수동으로 획득하고 로더의 라이선스( `https:` URL)와 콘텐츠 URL을 하드코딩합니다.

   예:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **대부분의 경우** 컨텐츠를 패키지할 때 컨텐츠의 ID를 고유하게 나타내는 `skd:` URL을 선택합니다. 로더에서 `skd:` URL을 분석한 다음 서버로 보내 토큰을 확보한 다음 결과 토큰을 URL로 사용합니다.

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

## TVSDK 애플리케이션에서 Apple FairPlay 사용 {#section_61CFA3C22FE64F52B2C8CE860B72E88B}

TVSDK 애플리케이션에서 Apple의 DRM 솔루션인 Apple FairPlay Streaming을 구현할 수 있습니다.

1. 구현하여 FairPlay 고객 리소스 로더를 만듭니다 `PTAVAssetResourceLoaderDelegate`. 자세한 내용은 TVSDK 애플리케이션에서 Apple FairPlay를 참조하십시오.

   >[!NOTE]
   >
   >FPS 인식 앱 *개발을 위한* FairPlay Server SDK에 포함되어 있는 FairPlay 스트리밍 프로그램 안내서 *(* FairPlayStreaming_PG.pdf [)의 지침을 따라야 합니다](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip).

   이 방법 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 은 안에 있는 것과 같습니다 `AVAssetResourceLoaderDelegate`.

   >[!NOTE]
   >
   >ExpressPlay 라이선스 서버 시나리오에서 콘텐트를 재생하려면 ExpressPlay FairPlay 서버 라이선스 요청 URL의 URL 체계를 (또는) `skd://` 에서 ( `https://` 또는 `https://`)로 변경합니다.

1. FairPlay *고객 리소스* 로더를 등록하십시오 `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

   >[!NOTE]
   >
   >FairPlay 라이선스 서버를 직접 작성하거나 타사 FairPlay 라이선스 서버를 사용하는 경우 라이선스 서버 공급업체에 문의하여 라이선스 서버 URL, 서식 및 기타 요구 사항을 확인하십시오.