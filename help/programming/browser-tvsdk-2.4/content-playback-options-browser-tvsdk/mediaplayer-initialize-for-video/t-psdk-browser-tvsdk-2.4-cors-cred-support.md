---
description: XMLHttpRequests의 withCredentials 속성을 지원하므로 다양한 요청 유형에 대해 CORS(교차 도메인 리소스 공유) 요청이 대상 도메인의 쿠키를 포함할 수 있습니다.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: XMLHttpRequests의 withCredentials 속성을 지원하므로 다양한 요청 유형에 대해 CORS(교차 도메인 리소스 공유) 요청이 대상 도메인의 쿠키를 포함할 수 있습니다.
seo-title: 교차 출처 리소스 공유
title: 교차 출처 리소스 공유
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 교차 출처 리소스 공유 {#cross-origin-resource-sharing}

XMLHttpRequests의 withCredentials 속성을 지원하므로 다양한 요청 유형에 대해 CORS(교차 도메인 리소스 공유) 요청이 대상 도메인의 쿠키를 포함할 수 있습니다.

클라이언트가 매니페스트, 세그먼트 또는 키를 요청하면 서버는 클라이언트가 후속 요청에 대해 전달해야 하는 쿠키를 설정할 수 있습니다. 쿠키를 읽고 쓸 수 있도록 허용하려면 클라이언트는 `withCredentials` 속성을 `true` 크로스 원본 요청에 대해 설정해야 합니다.

지정된 미디어 리소스를 재생할 때 대부분의 유형의 요청에 대한 `withCredentials` 지원을 활성화하려면

1. 개체를 `CORSConfig` 만듭니다.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 객체를 `corsConfig` 개체에 `NetworkConfiguration` 연결하고 로 `useCookieHeaderForAllRequests` 설정합니다 `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 개체에 `networkConfig` 설정합니다 `MediaPlayerItemConfig` .

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 메서드에 `MediaPlayerItemConfig` 전달합니다 `MediaPlayer.replaceCurrentResource` .

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>이 `useCookieHeaderForAllRequests` 플래그는 라이센스 요청에 영향을 주지 않습니다. 라이센스 요청에 대한 `withCredentials` 속성을 `true` 로 설정하려면 `withCredentials` 보호 데이터에 속성을 설정하거나 보호 데이터의 인증 키를 `httpRequestHeaders` 지정해야 합니다. 예:

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

일부 서버가 응답에서 필드를 와일드카드(&#39;*&#39;)로 설정하므로 플래그가 라이센스 요청에 영향을 주지 않습니다. `Access-Control-Allow-Origin` 그러나 자격 증명 플래그가 로 설정되어 `true`있으면 와일드카드를 사용할 수 없습니다 `Access-Control-Allow-Origin`. 모든 유형의 요청에 대해 `useCookieHeaderForAllRequests` `true` 로 설정하면 라이센스 요청에 대해 다음 오류가 표시될 수 있습니다.

다음 정보를 기억하십시오.

* 호출이 실패할 `withCredentials=true` 경우 브라우저 TVSDK는 호출 없이 다시 시도합니다 `withCredentials`.
* 로 호출이 수행되면 `networkConfiguration.useCookieHeaderForAllRequests=false`XHR 요청은 `withCredentials` 속성 없이 수행됩니다.