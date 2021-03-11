---
description: 대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
title: 대체 오디오 트랙 액세스
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 대체 오디오 트랙 {#access-alternate-audio-tracks} 액세스

대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.

1. `MediaPlayer`이(가) 적어도 `MediaPlayerStatus.PREPARED` 상태에 있을 때까지 기다립니다.
1. `MediaPlayerEvent.STATUS_CHANGED` 상태가 `MediaPlayerStatus.PREPARED`인 이벤트를 수신합니다.

   이 단계는 오디오 트랙의 초기 목록을 사용할 수 있음을 의미합니다.

1. `MediaPlayerItem` 인스턴스에서 사용 가능한 오디오 트랙을 가져옵니다.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (선택 사항) 사용 가능한 트랙을 사용자에게 표시합니다.
1. `MediaPlayerItem` 인스턴스에서 선택한 오디오 트랙을 설정합니다.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

