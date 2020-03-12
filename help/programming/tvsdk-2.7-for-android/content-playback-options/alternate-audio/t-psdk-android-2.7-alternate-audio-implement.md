---
description: 대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-description: 대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-title: 대체 오디오 트랙 액세스
title: 대체 오디오 트랙 액세스
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 대체 오디오 트랙 액세스 {#access-alternate-audio-tracks}

대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.

1. 적어도 상태가 `MediaPlayer` 될 때까지 `MediaPlayerStatus.PREPARED` 기다립니다.
1. 상태가 있는 `MediaPlayerEvent.STATUS_CHANGED` 이벤트를 수신합니다 `MediaPlayerStatus.PREPARED`.

   이 단계는 오디오 트랙의 초기 목록을 사용할 수 있음을 의미합니다.

1. 인스턴스에서 사용 가능한 오디오 트랙을 `MediaPlayerItem` 가져옵니다.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (선택 사항) 사용 가능한 트랙을 사용자에게 표시합니다.
1. 인스턴스에서 선택한 오디오 트랙을 `MediaPlayerItem` 설정합니다.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

