---
description: TVSDK는 스트림이 VOD(Video On Demand) 및 실시간 스트림에서 슬라이딩 윈도우 재생 목록인 특정 위치(시간)로의 검색을 지원합니다.
title: 현재 재생 위치에 검색 스크러빙 막대 표시
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 현재 재생 위치{#display-a-seek-scrub-bar-with-the-current-playback-position}와 함께 검색 스크러빙 막대 표시

TVSDK는 스트림이 VOD(Video On Demand) 및 실시간 스트림에서 슬라이딩 윈도우 재생 목록인 특정 위치(시간)로의 검색을 지원합니다.

>[!IMPORTANT]
>
>라이브 스트림에서 검색은 DVR에만 허용됩니다.

1. 검색을 위한 콜백을 설정합니다.

       검색은 비동기식이므로 TVSDK는 다음과 같은 검색 관련 이벤트를 전달합니다.
   
   * `SeekEvent.SEEK_BEGIN` - 시작을 찾습니다.
   * `SeekEvent.SEEK_END` - 성공적으로 검색
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - 사용자가 제공한 검색 위치를 재조정합니다.

1. 플레이어가 유효한 검색 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 중지됨 및 재생됩니다.

1. 사용자가 스크러빙 중일 때 해당 이벤트를 수신합니다.
1. 요청된 검색 위치(밀리초)를 `MediaPlayer.seek` 메서드에 전달합니다.

   ```
   function seek(position:Number):void;
   ```

   자산의 검색 가능한 기간에서만 검색할 수 있습니다. On-Demand 비디오의 경우 지속 시간은 0부터 자산의 지속 시간입니다.

   >[!TIP]
   >
   >이렇게 하면 재생 헤드가 스트림의 새 위치로 이동되지만 마지막으로 계산된 위치는 지정된 검색 위치와 다를 수 있습니다.

1. TVSDK가 `SeekEvent.SEEK_END` 이벤트를 전달할 때까지 기다립니다.
1. event.actualPosition을 사용하여 마지막으로 조정된 재생 위치를 검색합니다.

       검색 후 실제 시작 위치가 요청된 위치와 다를 수 있으므로 이 작업은 중요합니다. 다음과 같은 다양한 규칙이 적용될 수 있습니다.
   
   * 검색 또는 다른 위치 지정이 광고 브레이크 중간에 종료되거나 광고 분리를 건너뛰면 재생 비헤이비어가 영향을 받습니다.
   * 세그먼트 경계 근처에 있으면 검색 위치가 세그먼트의 시작으로 조정됩니다.

1. 검색 스크러빙 막대를 표시할 때 위치 정보를 사용합니다.
