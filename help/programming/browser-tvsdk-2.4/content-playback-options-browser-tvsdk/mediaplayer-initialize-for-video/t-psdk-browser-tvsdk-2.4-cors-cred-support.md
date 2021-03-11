---
description: XMLHttpRequests의 withCredentials 속성을 지원하므로 다양한 요청 유형에 대해 대상 도메인의 쿠키를 포함할 CORS(교차 도메인 리소스 공유) 요청을 허용합니다.
keywords: CORS;교차 도메인;리소스 공유;쿠키;자격 증명 포함
title: 원본 간 리소스 공유
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# 상호 원본 리소스 공유 {#cross-origin-resource-sharing}

XMLHttpRequests의 withCredentials 속성을 지원하므로 다양한 요청 유형에 대해 대상 도메인의 쿠키를 포함할 CORS(교차 도메인 리소스 공유) 요청을 허용합니다.

클라이언트가 매니페스트, 세그먼트 또는 키를 요청하면 서버는 클라이언트가 후속 요청에 대해 전달해야 하는 쿠키를 설정할 수 있습니다. 쿠키를 읽고 쓸 수 있도록 허용하려면 클라이언트는 상호 출처 요청에 대해 `withCredentials` 속성을 `true`으로 설정해야 합니다.

지정된 미디어 리소스를 재생할 때 대부분의 유형의 요청에 대해 `withCredentials` 지원을 활성화하려면:

1. `CORSConfig` 개체를 만듭니다.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. `corsConfig`을 `NetworkConfiguration` 개체에 첨부하고 `useCookieHeaderForAllRequests`를 `true`에 설정합니다.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. `MediaPlayerItemConfig` 개체에서 `networkConfig`을 설정합니다.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. `MediaPlayerItemConfig`을(를) `MediaPlayer.replaceCurrentResource` 메서드에 전달합니다.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>`useCookieHeaderForAllRequests` 플래그는 라이센스 요청에 영향을 주지 않습니다. 라이센스 요청에 대해 `withCredentials` 속성을 `true`으로 설정하려면 보호 데이터에 `withCredentials` 속성을 설정하거나 보호 데이터의 `httpRequestHeaders`에 인증 키를 지정해야 합니다. 예:

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

일부 서버에서 응답에서 `Access-Control-Allow-Origin` 필드를 와일드카드(&#39;*&#39;)로 설정했기 때문에 플래그는 라이선스 요청에 영향을 주지 않습니다. 그러나 자격 증명 플래그가 `true`으로 설정된 경우 와일드카드를 `Access-Control-Allow-Origin`에서 사용할 수 없습니다. 모든 유형의 요청에 대해 `useCookieHeaderForAllRequests`을 `true`으로 설정한 경우 라이센스 요청에 대해 다음 오류가 표시될 수 있습니다.

다음 정보를 기억하십시오.

* `withCredentials=true` 호출이 실패하면 브라우저 TVSDK가 `withCredentials` 없이 호출을 다시 시도합니다.
* `networkConfiguration.useCookieHeaderForAllRequests=false`으로 호출을 수행하면 `withCredentials` 특성 없이 XHR 요청이 수행됩니다.