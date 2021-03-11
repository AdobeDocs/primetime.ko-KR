---
title: 컨텐츠 제공
description: 컨텐츠 제공
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# 내용 {#delivering-content} 제공

Primetime DRM은 런타임이 네트워킹 레이어를 추상화하고 보호된 콘텐츠를 Primetime DRM 하위 시스템에 제공함에 따라 콘텐츠 전달 메커니즘에 영향을 받지 않습니다. 따라서 HTTP, HTTP Dynamic Streaming, RTMP 또는 RTMPE, HLS 등을 통해 컨텐츠를 전달할 수 있습니다.

그러나 프로토콜에 따라 보호된 내용의 메타데이터( `DRMContentData` - 일반적으로 사이드 로드한 [!DNL .metadata] 파일 형식)를 검색하는 것과 관련된 복잡성이 있을 수 있습니다. 이 DRM 메타데이터는 라이센스 사전 가져오기, DRM 인증 또는 장치 도메인 연결 등의 모든 `DRMManager` API를 호출하기 위해 필요합니다. 예를 들어 RTMP/RTMPE 프로토콜을 사용하면 FLV 및 F4V 데이터만 Flash Media Server(FMS)를 통해 클라이언트에 전달할 수 있습니다. 따라서 클라이언트는 다른 방법으로 메타데이터 Blob를 검색해야 합니다. 이 문제를 해결하기 위한 한 가지 방법은 HTTP 웹 서버에서 메타데이터를 호스팅하고, 재생되는 컨텐츠에 따라 적절한 메타데이터를 검색하도록 클라이언트 비디오 플레이어를 구현하는 것입니다.

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

