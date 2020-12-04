---
description: 기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 실시간 지점(DefaultMediaPlayer.LIVE_POINT)에서 시작됩니다.
seo-description: 기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 실시간 지점(DefaultMediaPlayer.LIVE_POINT)에서 시작됩니다.
seo-title: 특정 시간에 스트림 입력
title: 특정 시간에 스트림 입력
uuid: f58d908a-77b9-465f-b3a9-8fe63a249d39
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 특정 시간에 스트림 입력{#enter-a-stream-at-a-specific-time}

기본적으로 재생을 시작하면 VOD 미디어가 0부터 시작되고 실시간 미디어가 클라이언트 실시간 지점(DefaultMediaPlayer.LIVE_POINT)에서 시작됩니다.

위치를 `MediaPlayer.prepareToPlay`에 전달합니다.

TVSDK는 주어진 위치를 자산의 시작점으로 간주합니다. 검색 작업이 필요하지 않습니다. 위치가 검색 가능한 범위 내에 있지 않으면 기본 위치를 사용합니다.

예:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
