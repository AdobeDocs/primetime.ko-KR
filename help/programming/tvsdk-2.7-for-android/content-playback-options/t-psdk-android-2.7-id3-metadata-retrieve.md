---
description: ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.
seo-description: ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.
seo-title: ID3 태그
title: ID3 태그
uuid: 3fa199cd-668d-4d26-928f-074b6114b84c
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# ID3 태그 {#id-tags}

ID3 태그는 파일 제목이나 아티스트 이름과 같은 오디오 또는 비디오 파일에 대한 정보를 제공합니다. TVSDK는 HLS 스트림의 전송 스트림(TS) 세그먼트 수준에서 ID3 태그를 감지하고 이벤트를 전달합니다. 애플리케이션에서 태그에서 데이터를 추출할 수 있습니다.

>[!IMPORTANT]
>
>TVSDK는 오디오(AAC)에서 ID3 메타데이터(버전 2.3.0 또는 2.4.0)와 비디오(H.264) 스트림의 인코딩(ASCII, UTF8, UTF16-BE 또는 UTF16-LE)을 인식합니다. 인식된 버전 또는 형식 중 하나에 포함되지 않은 ID3 태그를 무시합니다. 지정되지 않은 인코딩은 UTF8로 처리됩니다.

TVSDK에서 ID3 메타데이터를 감지하면 다음 데이터가 포함된 알림을 발행합니다.

* TYPE = ID3
* NAME = ID3

1. 에 대한 이벤트 리스너를 `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` 구현하고 `MediaPlayer` 객체에 등록합니다.

   TVSDK는 `ID3` 메타데이터를 감지하면 이 수신기를 호출합니다.

   >[!TIP]
   >
   >사용자 지정 광고 큐는 동일한 `onTimedMetadata` 이벤트를 사용하여 새 태그 감지를 나타냅니다. 이렇게 하면 매니페스트 수준에서 사용자 지정 광고 큐가 검색되고 ID3 태그가 스트림에 포함되기 때문에 혼동이 발생하지 않습니다. 자세한 내용은 사용자 지정 [태그를 참조하십시오](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


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
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```

