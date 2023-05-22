---
description: ID3 태그는 파일 제목 또는 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션은 태그로부터 데이터를 추출할 수 있습니다.
title: ID3 태그
exl-id: a0b6ef0b-a8e1-44fa-ab34-3be60a2997c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# ID3 태그 {#id-tags}

ID3 태그는 파일 제목 또는 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션은 태그로부터 데이터를 추출할 수 있습니다.

>[!IMPORTANT]
>
>TVSDK는 오디오(AAC) 및 비디오(H.264) 스트림에서 가능한 인코딩(ASCII, UTF8, UTF16-BE 또는 UTF16-LE)으로 ID3 메타데이터(버전 2.3.0 또는 2.4.0)를 인식합니다. 인식된 버전 또는 형식 중 하나에 없는 ID3 태그는 무시됩니다. 지정되지 않은 인코딩은 UTF8로 처리됩니다.

TVSDK가 ID3 메타데이터를 감지하면 다음 데이터로 알림을 보냅니다.

* InfoCode = 303007
* 유형 = ID3
* 이름 = 없음
* ID = 0

1. 에 대한 이벤트 리스너 구현 `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 다음을 통해 등록: `MediaPlayer` 개체.

   TVSDK는 ID3 메타데이터를 감지하면 이 리스너를 호출합니다.

   >[!NOTE]
   >
   >사용자 정의 광고 큐는 동일한 `onTimedMetadata` 새 태그의 감지를 나타내는 이벤트입니다. 사용자 지정 광고 큐가 매니페스트 수준에서 검색되고 ID3 태그가 스트림에 포함되므로 혼동을 일으키지 않아야 합니다. 자세한 내용은 사용자 지정 태그 구성 을 참조하십시오.

1. 메타데이터를 검색합니다.

   ```java
   @Override 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
