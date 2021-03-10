---
description: 사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 재생 모드에 있는 것입니다. 트릭 재생 모드를 시작하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.
title: 빨리 전달 및 되감기 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# 빨리 구현 및 되감기 {#implement-fast-forward-and-rewind}

사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 재생 모드에 있는 것입니다. 트릭 재생 모드를 시작하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.

속도를 전환하려면 하나의 값을 설정해야 합니다.

1. `MediaPlayer`의 `rate` 속성을 허용된 값으로 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동합니다.

   * `MediaPlayerItem` 클래스는 허용되는 재생 속도를 정의합니다.
   * 지정된 요금이 허용되지 않을 경우 TVSDK에서 허용된 가장 가까운 비율을 선택합니다.

      트릭플레이 비율이 0(일시 중지) 또는 1(일반 재생)에서 1 또는 -1보다 작은 비율로 변경되면 타임라인의 모든 광고가 제거됩니다. 광고 위치를 중단하지 않고 컨텐츠를 빠르게 전달하여 재배치할 수 있도록 하기 위해 모든 타임라인에는 단 한 개의 기간만 있습니다. 이 작업은 TVSDK에 대한 타임라인 분리 동작으로 활성화되어 해결된 adBreaks를 모두 제거합니다. 0 또는 1에서 속임수가 다시 시작되면 먼저 타임라인 첨부 동작으로 adBreak가 복원됩니다.

      다음 정보를 기억하십시오.

   * trickplay 동작이 컨텐츠를 되감으려는 경우 속도가 1로 변경되면 재생이 다시 시작됩니다.
   * trickplay 동작이 컨텐츠를 빨리 전달하는 경우 마지막으로 건너뛰었던 adBreak가 다시 시작 위치에서 재생됩니다.

   이 예제에서는 플레이어의 내부 재생 속도를 요청된 속도로 설정합니다.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. 필요에 따라 비율 변경을 요청했을 때와 환율 변경이 실제로 발생할 때를 알려주는 비율 변경 이벤트를 수신할 수 있습니다.

   TVSDK는 트릭 플레이와 관련된 다음 이벤트를 전달합니다.

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 값을  `rate` 다른 값으로 변경하면

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 선택한 속도로 재생이 재개되는 경우입니다.

   TVSDK는 플레이어가 트릭 플레이 모드에서 일반 재생 모드로 돌아오면 이러한 두 이벤트를 전달합니다.

## 속도 변경 API 요소 {#rate-change-api}

TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이가 지원되는지 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 확인할 수 있는 방법, 속성 및 이벤트가 포함되어 있습니다.

다음 API 요소를 사용하여 재생 속도를 변경할 수 있습니다.

* `MediaPlayer.rate` setter 및 getter 함수 포함
* `MediaPlayer.localTime property` getter 함수 사용
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` getter 함수가 있는 속성
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` getter 함수가 있는 속성 - 유효한 속도를 지정합니다.

| 비율 값 | 재생 효과 |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | 지정된 승수가 정상보다 빠릅니다(예: 4가 정상보다 4배 빠름). |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | 빨리 되감기 모드로 전환 |
| 1.0 | 일반 재생 모드로 전환합니다. `play` 호출은 rate 속성을 1.0으로 설정하는 것과 같습니다. |
| 0.0 | 일시 중지(`pause` 호출은 rate 속성을 0.0으로 설정하는 것과 동일) |

## trick play {#limitations-behavior-trick-play} 의 제한 및 동작

트릭 재생 모드에 대한 제한 사항은 다음과 같습니다.

* 마스터 재생 목록에는 I-frame 전용 세그먼트가 포함되어야 합니다. I 프레임 트랙의 키 프레임만 화면에 표시됩니다.
* 오디오 트랙 및 닫힌 캡션이 비활성화됩니다.
* 응용 비트 전송률(ABR) 로직을 사용할 수 없습니다. TVSDK는 제공된 가장 낮은 속도와 800kbps 사이의 비트 전송률을 한 다음 트릭 플레이 세션 동안 이 속도를 사용합니다.
* 재생 및 일시 중지가 활성화됩니다.
* 검색은 허용되지 않습니다. 검색하려면 `pause`을(를) 호출하여 트릭 재생 모드를 종료한 다음 `seek`을(를) 호출합니다.

* trick-play 모드를 허용된 재생 속도(재생 또는 일시 중지)로 종료할 수 있습니다.
* 광고가 스트림에 통합되는 경우:

   * 메인 콘텐츠를 재생하는 동안에만 장난을 칠 수 있습니다. 광고 휴식 중에 trick play로 전환하려고 하면 오류가 전달됩니다.
   * 트릭 재생 모드를 시작한 후 광고 나누기가 무시되고 광고 이벤트가 실행되지 않습니다.
   * TVSDK에서 플레이어 애플리케이션에 노출한 타임라인은 광고 중단이 생략되어도 수정되지 않습니다.
   * `MediaPlayer.currentTime` 속성은 건너뛴 광고 중단의 지속 시간을 사용하여 앞으로(빨리 감기) 또는 뒤로(빨리 되감기) 이동합니다. 현재 시간에 대한 이러한 점프 동작을 사용하면 트릭 재생 동안 스트림 지속 시간이 변경되지 않은 상태로 유지됩니다. 플레이어 응용 프로그램은 `localTime` 속성을 사용하여 기본 콘텐트에 상대적인 시간을 추적할 수 있습니다. 광고를 건너뛰는 경우 로컬 시간에 대해 반환되는 값에 대해 시간 이동이 수행되지 않습니다.

   * `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` 이벤트는 광고 나누기를 건너뛸 바로 전에 전달됩니다. 플레이어는 이 이벤트를 사용하여 건너뛴 광고 중단과 관련된 사용자 지정 논리를 구현할 수 있습니다.
   * 기존 트릭 플레이는 검색을 종료할 때와 동일한 광고 재생 정책을 호출합니다.

      따라서 검색 에서와 마찬가지로 응용 프로그램의 재생 정책이 기본값과 다른지 여부에 따라 비헤이비어가 달라집니다. 기본적으로 트릭 플레이에서 벗어나 마지막으로 건너뛰었던 광고 브레이크가 재생됩니다.