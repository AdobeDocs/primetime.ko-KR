---
seo-title: 백그라운드 오디오 활성화
title: 백그라운드 오디오 활성화
uuid: aa6dc934-e85c-4db1-901b-9777f47106e6
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 백그라운드 오디오 활성화 {#enable-background-audio}

앱이 백그라운드에 있을 때 오디오 재생을 활성화하려면 플레이어가 준비된 `enableAudioPlaybackInBackground` 상태에서 true로 MediaPlayer의 API를 인수로 호출해야 합니다.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

휴대폰에 응답하는 등의 이벤트 중에 오디오 포커스가 끊기면 앱이 재생을 일시 중지해야 합니다. 다음 코드 조각은 `OnAudioFocusChangeListener`다음을 구현하는 방법을 보여 줍니다.

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
