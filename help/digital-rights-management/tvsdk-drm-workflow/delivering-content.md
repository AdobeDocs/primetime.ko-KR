---
title: 콘텐츠 제공
description: 콘텐츠 제공
copied-description: true
exl-id: a55293f0-ef9b-468f-a1b2-8222ebab0b4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 콘텐츠 제공 {#delivering-content}

Primetime DRM은 런타임이 네트워킹 계층을 추상화하고 보호된 콘텐츠를 Primetime DRM 하위 시스템에 단순히 제공하기 때문에 콘텐츠의 전달 메커니즘에 대해 불가지론적입니다. 따라서 HTTP, HTTP Dynamic Streaming, RTMP 또는 RTMPE, HLS 등을 통해 컨텐츠를 전달할 수 있습니다.

그러나 프로토콜에 따라 보호된 콘텐츠의 메타데이터 검색과 관련된 복잡한 문제가 있을 수 있습니다( `DRMContentData` 보통 사이드 로우드의 형태 [!DNL .metadata] file)을 참조하십시오. 이 DRM 메타데이터는 다음을 호출해야 합니다. `DRMManager` 라이선스 사전 가져오기, DRM 인증 또는 장치 도메인 연결과 같은 API. 예를 들어 RTMP/RTMPE 프로토콜을 사용하면 FLV 및 F4V 데이터만 Flash Media Server(FMS)를 통해 클라이언트에 전달할 수 있습니다. 이러한 이유로 클라이언트는 다른 방법으로 메타데이터 blob를 검색해야 합니다. 이 문제를 해결하기 위한 한 가지 옵션은 HTTP 웹 서버에서 메타데이터를 호스팅하고, 재생되는 콘텐츠에 따라 적절한 메타데이터를 검색하도록 클라이언트 비디오 플레이어를 구현하는 것입니다.

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```
