---
description: VOD 및 라이브 스트리밍에 대한 DVR을 지원하는 컨트롤 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.
title: DVR용으로 향상된 제어 막대 구성
exl-id: 8a764417-4425-44c0-9551-3077c8c0a323
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# DVR용으로 향상된 제어 막대 구성 {#construct-a-control-bar-enhanced-for-dvr}

VOD 및 라이브 스트리밍에 대한 DVR을 지원하는 컨트롤 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.

* VOD의 경우, 표시되는 창의 길이는 전체 자산의 기간입니다.
* 라이브 스트리밍의 경우 DVR(검색 가능) 창의 길이는 라이브 재생 창에서 시작하여 클라이언트 라이브 지점에서 끝나는 시간 범위로 정의됩니다.

   다음 정보를 숙지하십시오.

   * 클라이언트 라이브 포인트는 라이브 창 끝에서 버퍼된 길이를 뺀 값을 계산합니다.

      대상 기간은 매니페스트에서 조각의 최대 기간보다 크거나 같은 값입니다.
   * 기본값은 10000 ms입니다.
   * 라이브 재생을 위한 제어 표시줄에서는 재생을 시작할 때 먼저 클라이언트 라이브 포인트에 엄지 손가락을 배치하고, 찾기가 허용되지 않는 영역을 표시하는 영역을 표시하여 DVR을 지원합니다.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. DVR 지원을 사용하여 제어 표시줄을 구현하려면 [현재 재생 위치로 검색 스크러빙 막대 표시...](../../../tvsdk-2.7-for-android/content-playback-options/ui-configure/t-psdk-android-2.7-ui-seek-scrub-bar-display.md) 다음과 같은 차이점이 있습니다.

   * 재생 범위에 대해 대신 검색 가능한 범위에 대해서만 매핑되는 컨트롤 막대를 구현할 수 있습니다.

      검색에 대한 모든 사용자 상호 작용은 검색 가능한 범위에서 안전한 것으로 간주할 수 있습니다.
   * 재생 범위에 대해 매핑되지만 검색 가능한 범위도 표시하는 컨트롤 막대를 구현할 수 있습니다.

      컨트롤 막대의 경우:
   1. 재생 범위를 나타내는 오버레이를 제어 모음에 추가합니다.
   1. 사용자가 찾기를 시작할 때 원하는 찾기 위치가 `MediaPlayer.getSeekableRange`.

      For example:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      를 사용하여 클라이언트 Live Point를 찾도록 선택할 수도 있습니다 `MediaPlayer.LIVE_POINT` 상수.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
