---
description: 대체 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간에 전환할 수 있습니다. 사용자는 비디오가 재생될 때 원하는 언어 트랙을 선택할 수 있습니다.
title: 대체 오디오
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 개요 {#alternate-audio-overview}

대체 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간에 전환할 수 있습니다. 사용자는 비디오가 재생될 때 원하는 언어 트랙을 선택할 수 있습니다.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

TVSDK에서 다음을 만드는 경우 `MediaPlayerItem` 현재 비디오의 인스턴스에서는 `AudioTrack` 사용 가능한 각 오디오 트랙에 대한 항목입니다. 항목에 다음 항목이 포함되어 있습니다. `name` 속성은 일반적으로 해당 트랙의 언어에 대한 사용자가 인식할 수 있는 설명을 포함하는 문자열입니다. 이 항목에는 기본적으로 해당 트랙을 사용할지 여부에 대한 정보도 포함되어 있습니다. 비디오를 재생할 시간이 되면 사용 가능한 오디오 트랙 목록을 요청하고, 선택적으로 사용자가 트랙을 선택하고, 선택한 트랙으로 비디오를 재생하도록 설정할 수 있습니다.

>[!TIP]
>
>드문 경우이지만 TVSDK가 를 만든 후 추가 오디오 트랙을 사용할 수 있게 되는 경우에는 `MediaPlayerItem`, TVSDK가 `MediaPlayerItem.AUDIO_TRACK_UPDATED` 이벤트.

## 추가된 API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

대체 오디오를 지원하기 위해 다음 API가 추가되었습니다.

**`hasAlternateAudio`**

지정된 미디어에 기본 트랙이 아닌 대체 오디오 트랙이 있는 경우 이 부울 함수는 를 반환합니다 `true`. 대체 오디오 트랙이 없으면 이 함수는 를 반환합니다 `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

이 함수는 지정된 미디어에서 현재 사용 가능한 모든 오디오 트랙의 목록을 반환합니다.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

이 함수는 현재 선택한 대체 오디오 트랙과 언어 등의 속성을 반환합니다. 트랙의 자동 선택 사항도 추출할 수 있습니다.

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

이 기능은 재생할 대체 오디오 트랙을 선택합니다.

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
