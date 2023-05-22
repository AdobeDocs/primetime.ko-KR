---
title: 배경 오디오 활성화
description: 배경 오디오 활성화
copied-description: true
exl-id: db494969-ef63-46ad-9f08-a95f58c8b27b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# 배경 오디오 활성화 {#enable-background-audio}

앱이 백그라운드에 있을 때 오디오 재생을 활성화하려면 앱이 `enableAudioPlaybackInBackground` 플레이어가 PREPARED 상태에 있을 때 인수가 true인 MediaPlayer의 API입니다.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

앱은 전화에 응답하는 등의 이벤트 동안 오디오 포커스에 대한 유지가 상실되면 재생을 일시 중지해야 합니다. 다음 코드 조각은 다음을 구현하는 방법을 보여 줍니다. `OnAudioFocusChangeListener`:

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
