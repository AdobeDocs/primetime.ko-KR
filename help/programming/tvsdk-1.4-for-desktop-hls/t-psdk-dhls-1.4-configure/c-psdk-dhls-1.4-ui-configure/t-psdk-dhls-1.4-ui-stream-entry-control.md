---
description: 기본적으로 재생을 시작할 때 VOD 미디어는 0에 시작되고 라이브 미디어는 클라이언트 라이브 포인트에서 시작됩니다(DefaultMediaPlayer.LIVE_POINT).
title: 특정 시간에 스트림 입력
exl-id: b97dbabf-e2ab-4669-a9f3-9129af938a40
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 특정 시간에 스트림 입력{#enter-a-stream-at-a-specific-time}

기본적으로 재생을 시작할 때 VOD 미디어는 0에 시작되고 라이브 미디어는 클라이언트 라이브 포인트에서 시작됩니다(DefaultMediaPlayer.LIVE_POINT).

위치 전달 `MediaPlayer.prepareToPlay`.

TVSDK는 지정된 위치를 자산의 시작점으로 간주합니다. 검색 작업이 필요하지 않습니다. 위치가 검색 가능한 범위 내에 있지 않으면 에서는 기본 위치를 사용합니다.

예:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
