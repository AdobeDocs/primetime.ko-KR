---
title: 백그라운드 오디오 사용
description: 백그라운드 오디오 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 백그라운드 오디오 사용 {#enable-background-audio}

앱이 백그라운드에 있을 때 오디오 재생을 활성화하려면 플레이어가 준비 상태일 때 앱이 true로 MediaPlayer의 `enableAudioPlaybackInBackground` API를 인수로 호출해야 합니다.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

휴대폰에 응답하는 등의 이벤트 중에 오디오 포커스를 유지할 수 없는 경우 앱이 재생을 일시 중지해야 합니다. 다음 코드 조각은 `OnAudioFocusChangeListener`을 구현하는 방법을 보여 줍니다.

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

