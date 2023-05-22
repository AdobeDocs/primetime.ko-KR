---
description: TVSDK는 VOD(video on demand) 및 라이브 스트림 모두에서 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)로 이동하는 것을 지원합니다.
title: 현재 재생 위치에 검색 스크러빙 막대 표시
exl-id: a85a06d8-040e-435a-8f55-9df5af3babe1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 현재 재생 위치에 검색 스크러빙 막대 표시{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK는 VOD(video on demand) 및 라이브 스트림 모두에서 스트림이 슬라이딩 창 재생 목록인 특정 위치(시간)로 이동하는 것을 지원합니다.

>[!IMPORTANT]
>
>라이브 스트림에서의 찾기는 DVR에만 허용됩니다.

1. 찾기를 위한 콜백을 설정합니다.

       찾기는 비동기적이므로 TVSDK는 다음 찾기 관련 이벤트를 전달합니다.
   
   * `SeekEvent.SEEK_BEGIN` - 찾기 시작.
   * `SeekEvent.SEEK_END` - 검색 성공.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - 사용자가 제공한 찾기 위치를 재조정했습니다.

1. 플레이어가 찾기에 유효한 상태가 될 때까지 기다립니다.

   유효한 상태는 준비, 완료, 일시 정지됨 및 재생입니다.

1. 사용자가 스크러빙하는 시간을 확인하기 위해 적절한 이벤트를 수신합니다.
1. 요청한 찾기 위치(밀리초)를 `MediaPlayer.seek` 메서드를 사용합니다.

   ```
   function seek(position:Number):void;
   ```

   에셋의 검색 가능한 기간에서만 검색할 수 있습니다. Video on demand의 경우 지속 시간은 0부터 에셋의 지속 시간까지 입니다.

   >[!TIP]
   >
   >이렇게 하면 재생 헤드가 스트림의 새 위치로 이동하지만, 최종 계산된 위치는 지정된 검색 위치와 다를 수 있습니다.

1. TVSDK가 `SeekEvent.SEEK_END` 이벤트.
1. event.actualPosition을 사용하여 최종 조정된 재생 위치를 검색합니다.

       이것은 중요한 이유는 탐색 후의 실제 시작 위치가 요청된 위치와 다를 수 있기 때문이다. 다음을 포함한 다양한 규칙이 적용될 수 있습니다.
   
   * 검색 또는 기타 위치 변경이 광고 브레이크 중간에 종료되거나 광고 브레이크를 건너뛸 경우 재생 비헤이비어가 영향을 받습니다.
   * 세그먼트 경계 근처로 이동하면 찾기 위치가 세그먼트의 시작으로 조정됩니다.

1. 찾기 스크러빙 막대를 표시할 때 위치 정보를 사용합니다.
