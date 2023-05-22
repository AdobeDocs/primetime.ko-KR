---
description: XMLHttpRequests에서 withCredentials 특성을 지원하면 CORS(원본 간 리소스 공유) 요청이 다양한 요청 유형에 대한 대상 도메인의 쿠키를 포함할 수 있습니다.
keywords: CORS;원본 간;리소스 공유;쿠키;자격 증명 포함
title: 원본 간 리소스 공유
exl-id: 02826c87-b0c6-495b-a17d-67c5693a9772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 원본 간 리소스 공유 {#cross-origin-resource-sharing}

XMLHttpRequests에서 withCredentials 특성을 지원하면 CORS(원본 간 리소스 공유) 요청이 다양한 요청 유형에 대한 대상 도메인의 쿠키를 포함할 수 있습니다.

클라이언트가 매니페스트, 세그먼트 또는 키를 요청할 때 서버는 클라이언트가 후속 요청을 위해 전달해야 하는 쿠키를 설정할 수 있습니다. 쿠키를 읽고 쓸 수 있게 하려면 클라이언트는 `withCredentials` 특성 대상 `true` 원본 간 요청용.

활성화하려면 `withCredentials` 지정된 미디어 리소스를 재생할 때 대부분의 요청 유형 지원:

1. 만들기 `CORSConfig` 개체.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. 다음을 첨부합니다 `corsConfig` (으)로 `NetworkConfiguration` 오브젝트 및 세트 `useCookieHeaderForAllRequests` 끝 `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. 설정 `networkConfig` 다음에서 `MediaPlayerItemConfig` 개체.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. 합격 `MediaPlayerItemConfig` (으)로 `MediaPlayer.replaceCurrentResource` 메서드를 사용합니다.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>다음 `useCookieHeaderForAllRequests` 플래그는 라이선스 요청에 영향을 주지 않습니다. 을(를) 설정하려면 `withCredentials` 특성 대상 `true` 라이센스 요청의 경우 다음을 설정해야 합니다. `withCredentials` 보호 데이터에 특성을 지정하거나 `httpRequestHeaders` 보호 데이터. 예:

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

일부 서버에서 를 설정하므로 플래그는 라이선스 요청에 영향을 주지 않습니다. `Access-Control-Allow-Origin` 와일드카드(&#39;)에 대한 필드&#42;&#39;)를 입력합니다. 그러나 자격 증명 플래그가 로 설정되면 `true`, 와일드카드는 다음에서 사용할 수 없습니다. `Access-Control-Allow-Origin`. 다음을 설정하는 경우 `useCookieHeaderForAllRequests` 끝 `true` 모든 유형의 요청에서 라이선스 요청에 대해 다음 오류가 표시될 수 있습니다.

다음 정보를 숙지하십시오.

* 과(와) 통화한 경우 `withCredentials=true` 실패, 브라우저 TVSDK가 다음 작업 없이 호출을 재시도합니다. `withCredentials`.
* (으)로 호출되는 경우 `networkConfiguration.useCookieHeaderForAllRequests=false`, XHR 요청은 `withCredentials` 특성.
