---
description: 대체 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간을 전환할 수 있습니다. 비디오를 재생할 때 원하는 언어 트랙을 선택할 수 있습니다.
title: 대체 오디오
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 개요 {#alternate-audio-overview}

대체 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간을 전환할 수 있습니다. 비디오를 재생할 때 원하는 언어 트랙을 선택할 수 있습니다.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

TVSDK가 현재 비디오에 대한 `MediaPlayerItem` 인스턴스를 만들면 사용 가능한 각 오디오 트랙에 대해 `AudioTrack` 항목이 만들어집니다. 항목에 해당 트랙의 언어에 대한 사용자 인식 가능한 설명이 들어 있는 문자열인 `name` 속성이 포함되어 있습니다. 항목에는 기본적으로 해당 트랙을 사용할지 여부에 대한 정보도 포함되어 있습니다. 비디오를 재생할 시간이 되면 사용 가능한 오디오 트랙 목록을 요청하고 선택적으로 사용자가 트랙을 선택하도록 허용할 수 있으며 선택한 트랙으로 재생할 비디오를 설정할 수 있습니다.

>[!TIP]
>
>드물지만 TVSDK가 `MediaPlayerItem`을 만든 후 추가 오디오 트랙을 사용할 수 있게 되면 TVSDK가 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 이벤트를 실행합니다.

## API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE} 추가

다음 API가 대체 오디오를 지원하기 위해 추가되었습니다.

`hasAlternateAudio`

지정한 미디어에 기본 트랙이 아닌 대체 오디오 트랙이 있는 경우 이 부울 함수는 `true`을 반환합니다. 대체 오디오 트랙이 없으면 이 함수는 `false`을 반환합니다.

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

이 함수는 지정된 미디어에서 사용 가능한 현재 모든 오디오 트랙 목록을 반환합니다.

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

현재 선택된 대체 오디오 트랙과 언어 등의 속성을 반환하는 함수입니다. 트랙의 자동 선택을 추출할 수도 있습니다.

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

이 함수는 재생할 대체 오디오 트랙을 선택합니다.

```java
void selectAudioTrack(AudioTrack audioTrack);
```

예:

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```

