---
description: VOD 및 실시간 스트리밍에 대한 DVR 지원을 통해 제어 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.
seo-description: VOD 및 실시간 스트리밍에 대한 DVR 지원을 통해 제어 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.
seo-title: DVR에 대한 향상된 제어 막대 구성
title: DVR에 대한 향상된 제어 막대 구성
uuid: 08f943e8-90da-4860-92dd-dd289fd68cba
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# DVR에 대한 향상된 제어 막대 구성{#construct-a-control-bar-enhanced-for-dvr}

VOD 및 실시간 스트리밍에 대한 DVR 지원을 통해 제어 막대를 구현할 수 있습니다. DVR 지원에는 검색 가능한 창과 클라이언트 라이브 포인트의 개념이 포함됩니다.

* VOD의 경우, 검색 가능한 창의 길이는 전체 자산의 지속 시간입니다.
* 실시간 스트리밍의 경우 DVR(검색 가능) 창의 길이는 라이브 재생 창에서 시작하여 클라이언트 라이브 지점에서 끝나는 시간 범위로 정의됩니다.

   클라이언트 라이브 포인트는 라이브 창 끝의 버퍼된 길이를 뺀 값으로 계산됩니다. 대상 지속 시간은 매니페스트에 있는 조각의 최대 지속 기간보다 크거나 같은 값입니다.

   기본값은 10000ms입니다.

   라이브 재생을 위한 컨트롤 막대는 재생을 시작할 때 먼저 클라이언트 라이브 지점에 엄지 손가락을 놓고 검색이 허용되지 않는 영역을 표시하는 영역을 표시함으로써 DVR을 지원합니다.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. DVR 지원으로 제어 막대를 구현하려면 몇 가지 차이점과 함께 검색 스크럽 막대를 표시하는 단계를 수행합니다.

   * 재생 범위 대신 검색 가능한 범위에 대해서만 매핑되는 컨트롤 막대를 구현할 수 있습니다. 검색에 대한 모든 사용자 상호 작용은 검색 가능한 범위에서 안전한 것으로 간주될 수 있습니다.
   * 재생 범위에 대해 매핑되지만 검색 가능한 범위도 표시하는 컨트롤 막대를 구현하도록 선택할 수 있습니다.

      컨트롤 막대의 경우:
   1. 재생 범위를 나타내는 오버레이를 컨트롤 막대에 추가합니다.
   1. 사용자가 검색을 시작할 때 원하는 검색 위치가 `MediaPlayer.seekableRange` 속성을 사용하여 검색 가능한 범위 내에 있는지 확인합니다.

      예:

      ```
      var desiredPosition:Number = // TODO : choose a value 
      
      private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
          switch(event.status) { 
              case MediaPlayerStatus.PREPARED: 
                  _mediaPlayer.prepareToPlay(desiredPosition); 
          } 
      }
      ```

      또한 `MediaPlayer.LIVE_POINT` 상수를 사용하여 클라이언트 라이브 포인트를 찾도록 선택할 수 있습니다.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```


