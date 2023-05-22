---
description: 사용자가 미디어를 통해 빠르게 앞으로 감거나 빠르게 되감으면 트릭 플레이 모드가 됩니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1이 아닌 값으로 설정해야 합니다.
title: 신속한 전달 및 되감기 구현
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 신속한 전달 및 되감기 구현 {#implement-fast-forward-and-rewind}

사용자가 미디어를 통해 빠르게 앞으로 감거나 빠르게 되감으면 트릭 플레이 모드가 됩니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1이 아닌 값으로 설정해야 합니다.

속도를 전환하려면 하나의 값을 설정해야 합니다.

1. 를 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동 `rate` 다음에 대한 속성 `MediaPlayer` 을 입력합니다.

   * 다음 `MediaPlayerItem` 클래스는 허용된 재생 속도를 정의합니다.
   * TVSDK는 지정된 속도가 허용되지 않는 경우 가장 가까운 허용 속도를 선택합니다.

      속기 속도를 0(일시 중지) 또는 1(일반 재생)에서 1보다 크거나 -1보다 작은 속기로 변경하면 타임라인의 모든 광고가 제거됩니다. 전체 타임라인에는 광고 위치에서 멈추지 않고 콘텐츠를 빠르게 전달하고 되감도록 하는 트리크플레이 작업을 용이하게 하는 한 가지 기간만 있습니다. 이 작업은 TVSDK의 타임라인 분리 작업으로 해결된 모든 adBreak를 제거하여 사용할 수 있습니다. trickplay가 0 또는 1에서 다시 시작되면 타임라인 첨부 작업을 통해 adBreak가 먼저 복원됩니다.

      다음 정보를 숙지하십시오.

   * trickplay 작업이 콘텐츠를 되감는 것일 경우 속도가 1로 변경되면 재생이 다시 시작됩니다.
   * trickplay 작업이 콘텐츠를 빠르게 전달하는 것인 경우, 마지막으로 건너뛴 adBreak가 다시 시작 위치에서 재생됩니다.

   이 예제에서는 플레이어의 내부 재생 속도를 요청된 속도로 설정합니다.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 원할 경우 요금 변경을 요청한 시점과 요금 변경이 실제로 발생하는 시점을 알려주는 요금 변경 이벤트를 수신할 수 있습니다.

   TVSDK는 트릭 플레이와 관련된 다음 이벤트를 전달합니다.

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 다음과 같은 경우 `rate` 값이 다른 값으로 변경됩니다.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 선택한 속도로 재생이 다시 시작되는 때입니다.

   TVSDK는 플레이어가 trick-play 모드에서 일반 재생 모드로 돌아가면 이 두 이벤트를 모두 전달합니다.

## 속도 변경 API 요소 {#rate-change-api}

TVSDK에는 유효한 비율, 현재 비율, 트릭 플레이 지원 여부 및 앞으로 감기 및 되감기와 관련된 기타 기능을 결정하는 메서드, 속성 및 이벤트가 포함되어 있습니다.

다음 API 요소를 사용하여 재생 속도를 변경합니다.

* `MediaPlayer.rate` setter 및 getter 함수가 있는 속성
* `MediaPlayer.localTime property` getter 함수 포함
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` getter 함수가 있는 속성
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` getter 함수가 있는 속성 - 유효한 비율을 지정합니다.

| 비율 값 | 재생에 미치는 영향 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | 지정된 승수가 보통보다 빠르게(예: 4가 보통보다 4배 빠름) 빨리 감기 모드로 전환합니다. |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | 빠른 되감기 모드로 전환 |
| 1.0 | 일반 재생 모드로 전환(호출) `play` rate 속성을 1.0으로 설정하는 것과 같습니다.) |
| 0.0 | 일시 중지(호출) `pause` rate 속성을 0.0으로 설정하는 것과 같습니다.) |

## 트릭 플레이에 대한 제한 사항 및 동작 {#limitations-behavior-trick-play}

다음은 트릭 재생 모드의 제한 사항입니다.

* 마스터 재생 목록은 I-프레임 전용 세그먼트를 포함해야 합니다. I-프레임 트랙의 키 프레임만 화면에 표시됩니다.
* 오디오 트랙 및 폐쇄 캡션이 비활성화됩니다.
* ABR(적응형 비트 전송률) 논리를 사용할 수 없습니다. TVSDK는 제공된 최저 속도와 800kbps 사이의 비트 속도를 선택하고 전체 트릭 플레이 세션 동안 해당 속도를 사용합니다.
* 재생 및 일시 중지가 활성화됩니다.
* 찾기가 허용되지 않습니다. 찾으려면 를 호출하십시오. `pause` 트릭 재생 모드를 종료한 다음 를 호출하려면 `seek`.

* 허용된 재생 속도(재생 또는 일시 중지)로 트릭 재생 모드를 종료할 수 있습니다.
* 광고가 스트림에 통합되는 경우:

   * 주 콘텐츠를 재생하는 동안에만 트릭 플레이로 이동할 수 있습니다. 광고 브레이크 중에 트릭 플레이로 전환하려고 하면 오류가 표시됩니다.
   * 트릭 재생 모드를 시작한 후에는 광고 브레이크가 무시되고 광고 이벤트가 실행되지 않습니다.
   * TVSDK가 플레이어 애플리케이션에 노출하는 타임라인은 광고 브레이크를 건너뛴 경우에도 수정되지 않습니다.
   * 다음 `MediaPlayer.currentTime` 속성은 건너뛴 광고 브레이크 지속 시간에 따라 앞으로(빠르게 앞으로) 또는 뒤로(빠르게 되감기)로 이동합니다. 현재 시간에 대한 이 이동 동작은 트릭 플레이 중에 스트림 지속 시간을 수정하지 않은 상태로 유지할 수 있도록 한다. 플레이어 애플리케이션은 `localTime` 속성을 사용하여 기본 컨텐츠에만 상대적으로 시간을 추적할 수 있습니다. 광고를 건너뛸 때 로컬 시간에 대해 반환된 값에는 시간 이동이 수행되지 않습니다.

   * 다음 `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` ad break를 건너뛰기 직전에 이벤트가 발송됩니다. 플레이어는 이 이벤트를 사용하여 건너뛴 광고 브레이크와 관련된 사용자 지정 논리를 구현할 수 있습니다.
   * 트릭 재생을 종료하면 찾기를 종료할 때와 동일한 광고 재생 정책이 호출됩니다.

      따라서 찾기와 마찬가지로 동작은 애플리케이션의 재생 정책이 기본값과 다른지 여부에 따라 다릅니다. 기본적으로 마지막 생략된 광고 브레이크는 트릭 플레이에서 나온 지점에서 재생됩니다.
