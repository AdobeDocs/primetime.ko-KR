---
description: 이 예는 재생 타임라인에 사용자 정의 광고 마커를 포함하는 권장 방법을 보여줍니다.
seo-description: 이 예는 재생 타임라인에 사용자 정의 광고 마커를 포함하는 권장 방법을 보여줍니다.
seo-title: 타임라인에 사용자 정의 광고 마커 배치
title: 타임라인에 사용자 정의 광고 마커 배치
uuid: 47e31a97-e5da-46f3-bdcc-327c159c4355
translation-type: tm+mt
source-git-commit: 2a6ea34968ee7085931f99a24dfb23d097721b89
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# 사용자 지정 광고 마커를 타임라인 {#place-custom-ad-markers-on-the-timeline}에 배치

이 예는 재생 타임라인에 사용자 정의 광고 마커를 포함하는 권장 방법을 보여줍니다.

1. 대역 외 광고 배치 정보를 `RepaceTimeRange` 클래스의 목록/배열로 변환합니다.
1. `CustomRangeMetadata` 클래스의 인스턴스를 만들고, 해당 `setTimeRangeList` 메서드와 list/array를 인수로 사용하여 시간 범위 목록을 설정합니다.
1. 해당 `setType` 메서드를 사용하여 유형을 `MARK_RANGE`로 설정합니다.
1. `CustomRangeMetadata` 인스턴스와 함께 `MediaPlayerItemConfig.setCustomRangeMetadata` 메서드를 인수로 사용하여 사용자 지정 범위 메타데이터를 설정합니다.
1. `MediaPlayerItemConfig` 인스턴스와 함께 `MediaPlayer.replaceCurrentResource` 메서드를 인수로 사용하여 새 리소스를 현재 리소스로 설정합니다.
1. 플레이어가 `PREPARED` 상태임을 보고하는 `STATE_CHANGED` 이벤트를 기다립니다.
1. `MediaPlayer.play`을(를) 호출하여 비디오 재생을 시작합니다.

다음은 작업을 완료한 결과입니다.

* 예를 들어, 재생 타임라인에서 `ReplaceTimeRange`이 다른 항목과 겹치는 경우, `ReplaceTimeRange`의 시작 위치가 이미 배치된 종료 위치보다 이전 위치일 경우 TVSDK는 충돌을 피하기 위해 불쾌감을 주는 `ReplaceTimeRange`의 시작을 자동으로 조정합니다.

   이렇게 하면 조정된 `ReplaceTimeRange`이(가) 원래 지정한 것보다 짧습니다. 조정이 0으로 이어지는 경우 TVSDK가 자동으로 `ReplaceTimeRange`을(를) 삭제합니다.

* TVSDK는 사용자 지정 광고 중단에 대해 인접한 시간 범위를 찾아 별도의 광고 중단으로 묶습니다.

다른 시간 범위와 인접하지 않은 시간 범위는 단일 광고를 포함하는 광고 중단으로 변환됩니다.

* 컨텍스트 사용자 지정 광고 마커에서만 사용할 수 있는 `CustomRangeMetadata` 구성이 포함된 미디어 리소스를 로드하려고 하면 기본 자산이 VOD 유형이 아닌 경우 TVSDK에서 예외가 발생합니다.

* 사용자 지정 광고 마커를 처리할 때 TVSDK는 기타 광고 해결 메커니즘을 비활성화합니다(예: Adobe Primetime 광고 결정).

   모든 TVSDK 광고 해결 프로그램 모듈 또는 사용자 지정 광고 마커 메커니즘을 사용할 수 있습니다. 사용자 지정 광고 마커를 사용하면 광고 컨텐츠가 해결되어 타임라인에 배치됩니다.

다음 코드 조각은 타임라인에 사용자 정의 광고 마커로 세 개의 시간 범위를 배치합니다.

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
