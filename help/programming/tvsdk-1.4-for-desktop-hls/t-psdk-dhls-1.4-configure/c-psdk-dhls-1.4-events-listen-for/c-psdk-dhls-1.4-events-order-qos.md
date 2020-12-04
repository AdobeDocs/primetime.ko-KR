---
description: TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.
seo-description: TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.
seo-title: QoS 이벤트
title: QoS 이벤트
uuid: e6ba1e9b-435b-480d-bea9-bff41b4e0b21
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# QoS 이벤트{#qos-events}

TVSDK는 서비스 품질(QoS) 이벤트를 전달하여 버퍼링 및 검색 이벤트와 같은 QoS 통계 계산에 영향을 줄 수 있는 이벤트를 애플리케이션에 알립니다.

다음 예는 이러한 이벤트의 일반적인 진행 상태를 보여줍니다.

```
// For buffering 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_BEGIN, onBufferingBegin); 
private function onBufferingBegin(event:BufferEvent):void { ... } 
 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_END, onBufferingCompleted); 
private function onBufferingCompleted(event:BufferEvent):void { ... } 
 
// For seeking 
mediaPlayer.addEventListener(SeekEvent.SEEK_BEGIN, onSeekBegin); 
private function onSeekBegin(event:SeekEvent):void { ... } 
 
mediaPlayer.addEventListener(SeekEvent.SEEK_COMPLETED, onSeekCompleted); 
private function onSeekCompleted(event:SeekEvent):void { ... } 
 
...  SeekEvent.SEEK_POSITION_ADJUSTED...  //if the desired 
// seek position is modified by the current advertising policies 
```

