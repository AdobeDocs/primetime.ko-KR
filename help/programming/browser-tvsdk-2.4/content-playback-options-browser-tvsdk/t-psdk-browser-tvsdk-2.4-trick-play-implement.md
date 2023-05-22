---
description: 사용자가 미디어를 통해 빠르게 앞으로 감거나 빠르게 되감으면 트릭 플레이 모드가 됩니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1이 아닌 값으로 설정해야 합니다.
title: 신속한 전달 및 되감기 구현
exl-id: 21f9a3f6-1cae-4240-991d-c03a0e49adf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 신속한 전달 및 되감기 구현{#implement-fast-forward-and-rewind}

사용자가 미디어를 통해 빠르게 앞으로 감거나 빠르게 되감으면 트릭 플레이 모드가 됩니다. 트릭 재생 모드로 전환하려면 MediaPlayer 재생 속도를 1이 아닌 값으로 설정해야 합니다.

>[!IMPORTANT]
>
>* 트릭 재생 모드는 MPEG Dash 및 HLS VOD 컨텐츠에 대해서만 지원됩니다.
>* 트릭 재생 모드는 라이브 스트림 또는 광고에 지원되지 않습니다.
>* 기본 콘텐츠에서 광고로 전환할 때 브라우저 TVSDK는 트릭 재생 모드를 둡니다.
>


속도를 전환하려면 하나의 값을 설정해야 합니다.

1. 속도를 로 설정하여 일반 재생 모드(1x)에서 트릭 재생 모드로 이동합니다. `MediaPlayer` 을 입력합니다.

   * 다음 `MediaPlayerItem` 클래스는 허용된 재생 속도를 정의합니다.
   * 지정된 속도가 허용되지 않는 경우 브라우저 TVSDK가 가장 가까운 허용 속도를 선택합니다.

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

1. 원할 경우 요금 변경을 요청한 시점과 요금 변경이 실제로 발생하는 시점을 알려주는 요금 변경 이벤트를 수신할 수 있습니다.

       브라우저 TVSDK는 트릭 재생과 관련된 다음 이벤트를 전달합니다.
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` 다음과 같은 경우 `rate` 값이 다른 값으로 변경됩니다.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` 선택한 속도로 재생이 다시 시작되는 때입니다.

      플레이어가 trick-play 모드에서 일반 재생 모드로 돌아가면 브라우저 TVSDK가 이 두 이벤트를 모두 전달합니다.

## 속도 변경 API 요소 {#rate-change-API-elements}

브라우저 TVSDK에는 유효한 비율, 현재 비율, 트릭 플레이 지원 여부 및 앞으로 감기 및 되감기와 관련된 기타 기능을 결정하는 메서드, 속성 및 이벤트가 포함되어 있습니다.

다음 API 요소를 사용하여 재생 속도를 변경합니다.

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - 유효한 비율을 지정합니다.

   | 비율 값 | 재생에 미치는 영향 |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | 지정된 승수가 보통보다 빠르게(예: 4가 보통보다 4배 빠름) 빨리 감기 모드로 전환합니다. |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | 빠른 되감기 모드로 전환 |
   | 1.0 | 일반 재생 모드로 전환(호출) `play` rate 속성을 1.0으로 설정하는 것과 같습니다.) |
   | 0.0 | 일시 중지(호출) `pause` rate 속성을 0.0으로 설정하는 것과 같습니다.) |

## 트릭 플레이에 대한 제한 사항 및 동작 {#limitations-and-behavior-trick-play}

트릭 재생 모드가 작동하는 방식에는 몇 가지 제한 사항과 몇 가지 문제가 있습니다.

다음은 트릭 플레이 모드 제한 사항 목록입니다.

* 스트림에 트릭 플레이 적응이 포함되지 않으면 빠른 되감기가 비활성화되며, 빠른 포워드를 위한 최대 플레이 속도는 8로 제한됩니다.
* 트릭 재생 적응이 트릭 모드를 제공하는 데 사용될 때, 오디오 트랙은 비활성화된다.
* 트릭 재생 모드에서는 오디오 및 폐쇄 캡션 트랙 전환이 비활성화됩니다.
* 재생 및 일시 중지가 활성화됩니다.
* 찾기에서 재생이 트릭 재생 모드이면 재생 속도가 1로 설정되고 일반 재생이 다시 시작됩니다.
* 적응형 비트 전송률(ABR) 논리를 사용합니다.

   일반 적응을 사용할 때는 다음 기간 동안 프로필이 제한됩니다. `ABRControlParameters.minBitRate` 및 `ABRControlParameters.maxBitRate`. 트릭 플레이 적응을 사용할 때 프로필은 다음 기간 동안 제한됩니다. `ABRControlParameters.minTrickPlayBitRate` 및 `ABRControlParameters.maxTrickPlayBitRate`.
