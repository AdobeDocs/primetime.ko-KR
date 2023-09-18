---
description: 지연 바인딩 오디오는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되어 있으며 여러 대체 오디오 스트림을 포함할 수 있는 비디오를 재생합니다.
title: 대체 오디오 트랙 액세스
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 대체 오디오 트랙 액세스{#access-alternate-audio-tracks}

지연 바인딩 오디오는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되어 있으며 여러 대체 오디오 스트림을 포함할 수 있는 비디오를 재생합니다.

1. 다음을 기다리십시오. `MediaPlayer` 적어도 준비됨 상태여야 합니다.
1. 다음 이벤트를 수신합니다.

   * `MediaPlayerItemEvent.ITEM_CREATED`: 오디오 트랙의 초기 목록을 사용할 수 있습니다.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: 재생 중 오디오 트랙이 변경됨

1. 에서 사용 가능한 오디오 트랙 가져오기 `MediaPlayerItem` 인스턴스.
1. (선택 사항) 사용 가능한 트랙을 사용자에게 제공합니다.
1. 에서 선택한 오디오 트랙을 설정합니다. `MediaPlayerItem` 인스턴스.
