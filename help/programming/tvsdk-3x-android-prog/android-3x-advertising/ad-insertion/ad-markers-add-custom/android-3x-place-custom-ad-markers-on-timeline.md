---
description: 이 예는 재생 타임라인에 사용자 지정 광고 마커를 포함하는 권장 방법을 보여 줍니다.
title: 타임라인에 사용자 지정 광고 마커 배치
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 타임라인에 사용자 지정 광고 마커 배치 {#place-custom-ad-markers-on-the-timeline}

이 예는 재생 타임라인에 사용자 지정 광고 마커를 포함하는 권장 방법을 보여 줍니다.

1. 대역 외 광고 위치 정보를 목록/배열로 변환 `RepaceTimeRange` 클래스.
1. 의 인스턴스 만들기 `CustomRangeMetadata` 클래스 및 클래스 사용 `setTimeRangeList` 시간 범위 목록을 설정하는 인수로 list/array를 사용하는 메서드입니다.
1. 사용 `setType` 유형을 로 설정하는 방법 `MARK_RANGE`.
1. 사용 `MediaPlayerItemConfig.setCustomRangeMetadata` 을 사용하는 메서드 `CustomRangeMetadata` 인스턴스를 그 인수로 사용하여 사용자 지정 범위 메타데이터를 설정합니다.
1. 사용 `MediaPlayer.replaceCurrentResource` 을 사용하는 메서드 `MediaPlayerItemConfig` 인스턴스를 의 인수로 사용하여 새 리소스를 현재 리소스로 만듭니다.
1. 다음 시간 동안 대기 `STATE_CHANGED` 이벤트: 플레이어가 다음에 있음을 보고합니다. `PREPARED` 주.
1. 를 호출하여 비디오 재생 시작 `MediaPlayer.play`.

다음은 이 예제의 작업을 완료한 결과입니다.

* 다음과 같은 경우 `ReplaceTimeRange` 재생 타임라인에서 다른 재생 위치와 겹칩니다(예: 의 시작 위치). `ReplaceTimeRange` 이미 배치된 종료 위치보다 이전인 경우 TVSDK는 자동으로 위반의 시작을 조정합니다 `ReplaceTimeRange` 충돌을 피하려고.

  이렇게 하면 가 조정됩니다. `ReplaceTimeRange` 원래 지정한 것보다 짧습니다. 조정 시간이 0이면 TVSDK는 자동으로 위반을 중단합니다 `ReplaceTimeRange`.

* TVSDK는 사용자 지정 광고 브레이크에 대한 인접 시간 범위를 찾아 별도의 광고 브레이크로 클러스터링합니다.

다른 시간 범위와 인접하지 않은 시간 범위는 단일 광고가 포함된 광고 브레이크로 변환됩니다.

* 응용 프로그램이 구성에 이 포함된 미디어 리소스를 로드하려고 할 경우 `CustomRangeMetadata` tvsdk는 컨텍스트 사용자 지정 광고 마커에서만 사용할 수 있으며, 기본 자산이 VOD 유형이 아닌 경우 예외를 throw합니다.

* 사용자 지정 광고 마커를 처리할 때 TVSDK는 다른 광고 해결 메커니즘(예: Adobe Primetime 광고 결정)을 비활성화합니다.

  모든 TVSDK ad-resolver 모듈 또는 사용자 지정 광고 마커 메커니즘을 사용할 수 있습니다. 사용자 지정 광고 마커를 사용하면 광고 콘텐츠가 해결된 것으로 간주되어 타임라인에 배치됩니다.

다음 코드 조각은 타임라인에 세 개의 시간 범위를 사용자 지정 광고 마커로 배치합니다.

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
