---
description: VOD 및 라이브 스트리밍에 대한 DVR 지원을 통해 컨트롤 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.
title: DVR용으로 향상된 컨트롤 막대 구성
exl-id: a812f2d5-f1ee-4df6-9cc7-e39f55ec26f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# DVR용으로 향상된 컨트롤 막대 구성{#construct-a-control-bar-enhanced-for-dvr}

VOD 및 라이브 스트리밍에 대한 DVR 지원을 통해 컨트롤 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.

* VOD의 경우 검색 가능한 창의 길이는 전체 에셋의 기간입니다.
* 라이브 스트리밍의 경우, DVR(검색 가능) 창의 길이는 라이브 재생 창에서 시작하여 클라이언트 라이브 포인트에서 끝나는 시간 범위로 정의됩니다.

   클라이언트 라이브 포인트는 라이브 창 끝에서 버퍼된 길이를 빼서 계산됩니다. 대상 기간은 매니페스트에 있는 조각의 최대 기간보다 크거나 같은 값입니다.

   기본값은 10000ms입니다.

   라이브 재생을 위한 컨트롤 막대는 먼저 재생을 시작할 때 엄지 손가락을 클라이언트 라이브 포인트에 놓고 찾기가 허용되지 않는 영역을 표시하는 영역을 표시하여 DVR을 지원합니다.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. DVR 지원을 통해 컨트롤 막대를 구현하려면 몇 가지 사소한 차이점과 함께 찾기 스크러빙 막대를 표시하는 단계를 따르십시오.

   * 재생 범위가 아니라 검색 가능 범위에 대해서만 매핑된 제어 모음을 구현하도록 선택할 수 있습니다. 찾기에 대한 모든 사용자 상호 작용은 검색 가능한 범위에서 안전한 것으로 간주될 수 있습니다.
   * 재생 범위에 대해 매핑되지만 검색 가능한 범위도 표시하는 컨트롤 막대를 구현하도록 선택할 수 있습니다.

      컨트롤 막대의 경우
   1. 재생 범위를 나타내는 컨트롤 막대에 오버레이를 추가합니다.
   1. 사용자가 찾기를 시작할 때 를 사용하여 원하는 찾기 위치가 찾을 수 있는 범위 내에 있는지 확인합니다. `MediaPlayer.getSeekableRange`.

      예:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      를 사용하여 클라이언트 라이브 포인트를 찾도록 선택할 수도 있습니다. `MediaPlayer.LIVE_POINT` 일정합니다.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
