---
description: 사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 재생 모드에 있는 것입니다. 트릭 재생 모드를 시작하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.
title: 빨리 전달 및 되감기 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# 빨리 전달 및 되감기{#implement-fast-forward-and-rewind}

사용자가 미디어를 빨리 되감거나 빨리 되감으면 트릭 재생 모드에 있는 것입니다. 트릭 재생 모드를 시작하려면 MediaPlayer 재생 속도를 1 이외의 값으로 설정해야 합니다.

>[!IMPORTANT]
>
>* 트릭 재생 모드는 MPEG 대시 및 HLS VOD 컨텐츠에만 지원됩니다.
>* 트릭 재생 모드는 라이브 스트림 또는 광고에 대해 지원되지 않습니다.
>* 기본 컨텐츠에서 광고로 전환하는 경우 브라우저 TVSDK는 트릭 플레이 모드를 유지합니다.

>



속도를 전환하려면 하나의 값을 설정해야 합니다.

1. `MediaPlayer`의 속도를 허용된 값으로 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동합니다.

   * `MediaPlayerItem` 클래스는 허용되는 재생 속도를 정의합니다.
   * 지정된 속도가 허용되지 않는 경우 브라우저 TVSDK에서 허용된 가장 가까운 속도를 선택합니다.

      다음 예제 함수는 비율을 설정합니다.

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      다음 예제 함수를 사용하여 사용 가능한 재생 속도를 쿼리할 수 있습니다.

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. 필요에 따라 비율 변경을 요청했을 때와 환율 변경이 실제로 발생할 때를 알려주는 비율 변경 이벤트를 수신할 수 있습니다.

       브라우저 TVSDK는 트릭 플레이와 관련된 다음 이벤트를 전달합니다.
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 값을  `rate` 다른 값으로 변경하면

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 선택한 속도로 재생이 재개되는 경우입니다.

      브라우저 TVSDK는 플레이어가 트릭 플레이 모드에서 일반 재생 모드로 돌아오면 이러한 두 이벤트를 전달합니다.

## 속도 변경 API 요소 {#rate-change-API-elements}

브라우저 TVSDK에는 유효한 속도, 현재 속도, 트릭 플레이 지원 여부 및 빨리 감기 및 되감기와 관련된 기타 기능을 확인할 수 있는 방법, 속성 및 이벤트가 포함되어 있습니다.

다음 API 요소를 사용하여 재생 속도를 변경할 수 있습니다.

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - 유효한 속도를 지정합니다.

   | 비율 값 | 재생 효과 |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | 지정된 승수가 정상보다 빠릅니다(예: 4가 정상보다 4배 빠름). |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | 빨리 되감기 모드로 전환 |
   | 1.0 | 일반 재생 모드로 전환합니다. `play` 호출은 rate 속성을 1.0으로 설정하는 것과 같습니다. |
   | 0.0 | 일시 중지(`pause` 호출은 rate 속성을 0.0으로 설정하는 것과 동일) |

## trick-play {#limitations-and-behavior-trick-play}에 대한 제한 및 동작

트릭 재생 모드가 동작하는 방법에는 몇 가지 제한 사항과 몇 가지 문제가 있습니다.

다음은 트릭 플레이 모드 제한 사항의 목록입니다.

* 스트림에 트릭 재생 적응이 포함되어 있지 않으면 [빨리 되감기]가 비활성화되고 [빨리 감기]에 대한 최대 재생 속도는 8로 제한됩니다.
* trick play 어댑터를 사용하여 트릭 모드를 제공하면 오디오 트랙이 비활성화됩니다.
* 트릭 재생 모드에서 오디오 및 닫힌 캡션 트랙의 전환이 비활성화됩니다.
* 재생 및 일시 중지가 활성화됩니다.
* 검색 시 재생 모드가 트릭 재생 모드인 경우 재생 속도가 1로 설정되고 정상적인 재생 상태가 다시 시작됩니다.
* 응용 비트 전송률(ABR) 로직을 사용할 수 있습니다.

   일반 어댑터를 사용할 때 프로필은 `ABRControlParameters.minBitRate`과 `ABRControlParameters.maxBitRate` 사이에 제한됩니다. trick play 어댑터를 사용하는 경우 프로필은 `ABRControlParameters.minTrickPlayBitRate`과 `ABRControlParameters.maxTrickPlayBitRate` 사이에 제한됩니다.