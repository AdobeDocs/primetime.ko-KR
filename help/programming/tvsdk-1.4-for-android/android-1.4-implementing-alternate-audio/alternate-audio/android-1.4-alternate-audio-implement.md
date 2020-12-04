---
description: 늦게 바인딩 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 여러 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-description: 늦게 바인딩 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 여러 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.
seo-title: 대체 오디오 트랙 액세스
title: 대체 오디오 트랙 액세스
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# 대체 오디오 트랙 액세스{#access-alternate-audio-tracks}

늦게 바인딩 오디오에서는 MediaPlayer를 사용하여 M3U8 HLS 재생 목록에 지정되고 여러 개의 대체 오디오 스트림이 포함될 수 있는 비디오를 재생합니다.

1. MediaPlayer가 적어도 PREPARED 상태가 될 때까지 기다립니다.
1. 이 이벤트에 대한 의견 수렴:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`:오디오 트랙의 초기 목록을 사용할 수 있습니다.

1. `MediaPlayerItem` 인스턴스에서 사용 가능한 오디오 트랙을 가져옵니다.

   `mediaPlayerItem.getAudioTracks()` 1. (선택 사항) 사용 가능한 트랙을 사용자에게 제공합니다.
1. `MediaPlayerItem` 인스턴스에서 선택한 오디오 트랙을 설정합니다.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`