---
description: TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.
seo-description: TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.
seo-title: 비디오 지속 시간, 현재 시간 및 남은 시간 표시
title: 비디오 지속 시간, 현재 시간 및 남은 시간 표시
uuid: 64536ba7-33a1-49f8-a947-5700e1e9c032
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 비디오{#display-the-duration-current-time-and-remaining-time-of-the-video}의 지속 시간, 현재 시간 및 남은 시간을 표시합니다.

TVSDK를 사용하여 검색 막대에 표시할 수 있는 미디어에 대한 정보를 검색할 수 있습니다.

1. 플레이어가 INITIALIZED 상태가 될 때까지 기다립니다.
1. `MediaPlayer.currentTime` 속성을 사용하여 현재 재생 헤드 시간을 검색합니다.

   가상 타임라인에서 현재 재생 헤드 위치를 밀리초 단위로 반환합니다. 여러 광고나 광고 분리가 기본 스트림에 분할되는 등 대체 컨텐츠의 여러 인스턴스가 포함될 수 있는 해결된 스트림에 대해 시간을 계산합니다. 라이브/선형 스트림의 경우 반환된 시간은 항상 재생 창 범위에 있습니다.

   ```
   function get currentTime():Number;
   ```

1. 스트림의 재생 범위를 검색하고 지속 시간을 결정합니다.
   1. `mediaPlayer.playbackRange` 속성을 사용하여 가상 타임라인 시간 범위를 가져옵니다.

      ```
      function get playbackRange():TimeRange;
      ```

   1. `mediacore.utils.TimeRange`을(를) 사용하여 시간 범위를 분석합니다.
   1. 지속 기간을 결정하려면 범위 끝에서 시작을 빼십시오.

      여기에는 스트림에 삽입되는 추가 컨텐츠 기간이 포함됩니다(광고).

      VOD의 경우 범위는 항상 0으로 시작하고 종료 값은 기본 컨텐츠 지속 기간의 합계와 스트림(광고)에 삽입된 추가 컨텐츠 지속 시간을 합한 것입니다.

      선형/라이브 에셋의 경우 범위는 재생 창 범위를 나타내며 이 범위는 재생 중에 변경됩니다.

      TVSDK는 미디어 항목을 새로 고치고 해당 속성(재생 범위 포함)이 업데이트되었음을 나타내는 `MediaPlayerItemEvent.ITEM_UPDATED` 이벤트를 전달합니다.

1. 검색 막대 매개 변수를 설정하려면 `MediaPlayer` 및 Flex SDK에서 공개적으로 사용할 수 있는 `HSlider` 클래스에서 사용할 수 있는 메서드를 사용하십시오.

1. 타이머를 사용하여 현재 시간을 주기적으로 검색하고 `SeekBar`을 업데이트합니다.
