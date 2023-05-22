---
description: 대체 또는 지연 바인딩 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간에 전환할 수 있습니다. 이러한 방식으로, 사용자는 비디오가 재생될 때 언어 트랙을 선택할 수 있다.
title: 대체 오디오
exl-id: ce3dbdd3-9cc2-4732-b980-33b091667f70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 대체 오디오 {#alternate-audio}

대체 또는 지연 바인딩 오디오를 사용하면 비디오 트랙에 사용할 수 있는 오디오 트랙 간에 전환할 수 있습니다. 이러한 방식으로, 사용자는 비디오가 재생될 때 언어 트랙을 선택할 수 있다.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

TVSDK에서 다음을 만드는 경우 `MediaPlayerItem` 현재 비디오의 인스턴스에서는 `AudioTrack` 사용 가능한 각 오디오 트랙에 대한 항목입니다. 항목에 다음 항목이 포함되어 있습니다. `name` 속성은 일반적으로 해당 트랙의 언어에 대한 사용자가 인식할 수 있는 설명을 포함하는 문자열입니다. 이 항목에는 기본적으로 해당 트랙을 사용할지 여부에 대한 정보도 포함되어 있습니다.

비디오를 재생할 시간이 되면 사용 가능한 오디오 트랙 목록을 요청하고, 선택적으로 사용자가 하나를 선택하도록 하고, 선택한 트랙으로 비디오를 재생하도록 설정할 수 있습니다.

드문 경우이지만 추가 오디오 트랙이 만들어진 후 사용할 수 있게 되는 경우 `MediaPlayerItem`, TVSDK가 `MediaPlayerItem.AUDIO_UPDATED` 이벤트.

## 추가된 API {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

대체 오디오를 지원하기 위해 다음 API가 추가되었습니다.

`hasAlternateAudio`

지정된 미디어에 기본 트랙이 아닌 대체 오디오 트랙이 있는 경우 이 부울 함수는 를 반환합니다 `true`. 대체 오디오 트랙이 없으면 이 함수는 를 반환합니다 `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

이 함수는 지정된 미디어에서 현재 사용 가능한 모든 오디오 트랙의 목록을 반환합니다.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
if (_audioTracks) { 
    out = _audioTracks; 
    out->addRef(); 
    return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

`getSelectedAudioTrack`

이 함수는 현재 선택한 대체 오디오 트랙과 언어 등의 속성을 반환합니다. 트랙의 자동 선택 사항도 추출할 수 있습니다.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

이 기능은 재생할 대체 오디오 트랙을 선택합니다.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
