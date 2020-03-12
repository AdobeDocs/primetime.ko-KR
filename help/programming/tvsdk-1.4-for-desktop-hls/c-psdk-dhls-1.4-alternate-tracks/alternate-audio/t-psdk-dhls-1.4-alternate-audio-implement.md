---
description: 늦게 바인딩 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-description: 늦게 바인딩 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-title: 대체 오디오 트랙 액세스
title: 대체 오디오 트랙 액세스
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 대체 오디오 트랙 액세스{#access-alternate-audio-tracks}

늦게 바인딩 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.

1. READY 상태 `MediaPlayer` 이상을 기다립니다.
1. 다음 이벤트에 대한 의견 수렴:

   * `MediaPlayerItemEvent.ITEM_CREATED`:오디오 트랙의 초기 목록을 사용할 수 있습니다.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`:재생 중에 변경된 오디오 트랙

1. 인스턴스에서 사용 가능한 오디오 트랙을 `MediaPlayerItem` 가져옵니다.
1. (선택 사항) 사용 가능한 트랙을 사용자에게 표시합니다.
1. 인스턴스에서 선택한 오디오 트랙을 `MediaPlayerItem` 설정합니다.
