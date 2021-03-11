---
description: VOD 및 실시간 스트리밍에 대한 DVR 지원을 통해 제어 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창의 개념과 클라이언트 라이브 지점이 포함됩니다.
title: DVR에 대한 향상된 제어 막대 구성
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# DVR {#construct-a-control-bar-enhanced-for-dvr}에 대해 향상된 제어 막대 구성

VOD 및 실시간 스트리밍에 대한 DVR 지원을 통해 제어 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창의 개념과 클라이언트 라이브 지점이 포함됩니다.

* VOD의 경우, 검색 가능한 창의 길이는 전체 자산의 지속 시간입니다.
* 실시간 스트리밍의 경우 DVR(검색 가능) 창의 길이는 라이브 재생 창에서 시작하여 클라이언트 라이브 지점에서 끝나는 시간 범위로 정의됩니다.

   다음 정보를 기억하십시오.

   * 클라이언트 라이브 포인트는 라이브 윈도우 끝에서 버퍼링된 길이를 제거하여 계산됩니다.

      대상 지속 시간은 매니페스트에 있는 조각의 최대 지속 시간보다 크거나 같은 값입니다.
   * 기본값은 10000ms입니다.
   * 라이브 재생의 제어 막대는 재생을 시작할 때 먼저 클라이언트 라이브 지점에 엄지를 놓고 검색이 허용되지 않는 영역을 표시하는 영역을 표시함으로써 DVR을 지원합니다.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. DVR을 지원하는 컨트롤 막대를 구현하려면 [현재 재생 위치로 검색 스크러빙 막대 표시의 단계를 따릅니다.](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) 다음과 같은 차이점이 있습니다.

   * 재생 범위 대신 검색 가능한 범위에 대해서만 매핑되는 컨트롤 막대를 구현할 수 있습니다.

      검색에 대한 모든 사용자 상호 작용은 검색 가능한 범위에서 안전한 것으로 간주할 수 있습니다.
   * 재생 범위에 대해 매핑되지만 검색 가능한 범위도 표시하는 컨트롤 막대를 구현할 수 있습니다.

      컨트롤 막대의 경우:
   1. 재생 범위를 나타내는 오버레이를 컨트롤 막대에 추가합니다.
   1. 사용자가 검색을 시작할 때 원하는 검색 위치가 `MediaPlayer.getSeekableRange`을(를) 사용하여 검색 가능한 범위 내에 있는지 확인합니다.

      예:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      `MediaPlayer.LIVE_POINT` 상수를 사용하여 클라이언트 라이브 지점을 찾도록 선택할 수도 있습니다.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
