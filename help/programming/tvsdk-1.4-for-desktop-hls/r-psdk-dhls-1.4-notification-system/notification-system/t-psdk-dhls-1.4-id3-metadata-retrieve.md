---
description: ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.
seo-description: ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.
seo-title: ID3 태그
title: ID3 태그
uuid: 5c016260-5ced-480e-897a-11ffe7f34441
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# ID3 태그{#id-tags}

ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.

>[!IMPORTANT]
>
>TVSDK는 가능한 인코딩(ASCII, UTF8, UTF16-BE 또는 UTF16-LE)에서 오디오(AAC) 및 비디오(H.264) 스트림의 ID3 메타데이터(버전 2.3.0 또는 2.4.0)를 인식합니다. 인식된 버전 또는 형식 중 하나에 포함되지 않은 ID3 태그를 무시합니다. 지정되지 않은 인코딩은 UTF8로 처리됩니다.

TVSDK에서 ID3 메타데이터를 감지하면 다음 데이터가 포함된 알림을 발행합니다.

* InfoCode = 303007
* TYPE = ID3
* NAME = 없음
* ID = 0

1. `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`에 대한 이벤트 리스너를 구현하고 `MediaPlayer` 개체에 등록합니다.

   TVSDK는 ID3 메타데이터를 감지하면 이 수신기를 호출합니다.

   >[!NOTE]
   >
   >사용자 지정 광고 큐는 동일한 `onTimedMetadata` 이벤트를 사용하여 새 태그 탐지를 나타냅니다. 이로 인해 매니페스트 수준에서 사용자 지정 광고 큐가 검색되고 ID3 태그가 스트림에 포함되기 때문에 혼란이 발생해서는 안됩니다. 자세한 내용은 사용자 지정 태그 구성을 참조하십시오.

1. 메타데이터를 검색합니다.

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   ```

