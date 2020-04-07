---
description: 이 예는 재생 타임라인에 사용자 정의 광고 마커를 포함하는 권장 방법을 보여줍니다.
seo-description: 이 예는 재생 타임라인에 사용자 정의 광고 마커를 포함하는 권장 방법을 보여줍니다.
seo-title: 타임라인에 사용자 정의 광고 마커 배치
title: 타임라인에 사용자 정의 광고 마커 배치
uuid: ee74d1f3-7186-44b8-bad7-55af579842e8
translation-type: tm+mt
source-git-commit: 9f1f27bc6c23994338775a32f978a2e768a0f3aa

---


# 타임라인에 사용자 정의 광고 마커 배치 {#place-custom-ad-markers-on-the-timeline}

이 예는 재생 타임라인에 사용자 정의 광고 마커를 포함하는 권장 방법을 보여줍니다.

1. 대역 외 광고 배치 정보를 `RepaceTimeRange` 클래스 목록/배열로 변환합니다.
1. 클래스 인스턴스를 만들고, 목록/배열과 함께 해당 `CustomRangeMetadata` `setTimeRangeList` 메서드를 인수로 사용하여 시간 범위 목록을 설정합니다.
1. 이 `setType` 메서드를 사용하여 형식을 로 설정합니다 `MARK_RANGE`.
1. 인스턴스와 함께 `MediaPlayerItemConfig.setCustomRangeMetadata` `CustomRangeMetadata` 메서드를 인수로 사용하여 사용자 지정 범위 메타데이터를 설정합니다.
1. 인스턴스와 함께 `MediaPlayer.replaceCurrentResource` `MediaPlayerItemConfig` 메서드를 인수로 사용하여 새 리소스를 현재 리소스로 설정합니다.
1. 플레이어가 `STATE_CHANGED` `PREPARED` 상태에 있다고 보고하는 이벤트를 기다립니다.
1. 전화하여 비디오 재생을 시작합니다 `MediaPlayer.play`.

다음은 이 예제의 작업을 완료한 결과입니다.>
* 예를 들어 재생 타임라인에서 다른 `ReplaceTimeRange` 요소와 겹치는 경우, 시작 위치가 이미 배치된 끝 위치보다 이전인 `ReplaceTimeRange` `ReplaceTimeRange` 경우 TVSDK는 충돌을 피하기 위해 불쾌감을 주는 시작 부분을 자동으로 조정합니다.

   이렇게 하면 조정된 내용이 원래 지정된 것보다 `ReplaceTimeRange` 짧습니다. 조정이 0으로 이어지면 TVSDK가 자동으로 문제가 `ReplaceTimeRange`없어집니다.

* TVSDK는 사용자 지정 광고 분리에 대해 인접한 시간 범위를 찾아 별도의 광고 분리로 클러스터합니다.

   다른 시간 범위와 인접하지 않은 시간 범위는 단일 광고를 포함하는 광고 중단으로 변환됩니다.
* 애플리케이션이 컨텍스트 사용자 지정 광고 마커에서만 사용할 수 `CustomRangeMetadata` 있는 구성이 포함된 미디어 리소스를 로드하려고 하면 기본 자산이 VOD 유형이 아닌 경우 TVSDK에서 예외가 발생합니다.
* 맞춤형 광고 마커를 처리할 때 TVSDK는 기타 광고 해결 메커니즘(예: Adobe Primetime 광고 결정)을 비활성화합니다.

   모든 TVSDK 광고 해결 프로그램 모듈 또는 사용자 지정 광고 마커 메커니즘을 사용할 수 있습니다. 사용자 지정 광고 마커를 사용하면 광고 컨텐츠가 해결되어 타임라인에 배치됩니다.

다음 코드 조각은 타임라인에 사용자 지정 광고 마커로 세 개의 시간 범위를 배치합니다.

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
