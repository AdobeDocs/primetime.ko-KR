---
description: 대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-description: 대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-title: 대체 오디오 트랙 액세스
title: 대체 오디오 트랙 액세스
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# 대체 오디오 트랙 액세스{#access-alternate-audio-tracks}

대체 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 몇 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.

1. `MediaPlayer`이(가) `MediaPlayerStatus.PREPARED` 상태 이상이어야 합니다.
1. `MediaPlayerEvent.STATUS_CHANGED` 상태가 `MediaPlayerStatus.PREPARED`인 이벤트를 수신합니다.

   이 단계는 오디오 트랙의 초기 목록을 사용할 수 있음을 의미합니다.

1. `MediaPlayerItem` 인스턴스에서 사용 가능한 오디오 트랙을 가져옵니다.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (선택 사항) 사용 가능한 트랙을 사용자에게 제공합니다.
1. `MediaPlayerItem` 인스턴스에서 선택한 오디오 트랙을 설정합니다.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
