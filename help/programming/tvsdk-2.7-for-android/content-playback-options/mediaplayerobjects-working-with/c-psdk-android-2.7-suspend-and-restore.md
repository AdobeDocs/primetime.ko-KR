---
description: 장치 화면이 꺼지고 켜져 있을 때 TVSDK MediaPlayer 일시 중단 및 복원은 애플리케이션에서 처리해야 합니다.
keywords: SurfaceView;Suspend;Restore;BroadcastReceiver
seo-description: 장치 화면이 꺼지고 켜져 있을 때 TVSDK MediaPlayer 일시 중단 및 복원은 애플리케이션에서 처리해야 합니다.
seo-title: MediaPlayer 일시 중단 및 복원
title: MediaPlayer 일시 중단 및 복원
uuid: 7777af91-547c-4f7a-8818-3d46dccee7d6
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# MediaPlayer 일시 중단 및 복원 {#suspend-and-restore-mediaplayer}

장치 화면이 꺼지고 켜져 있을 때 TVSDK MediaPlayer 일시 중단 및 복원은 애플리케이션에서 처리해야 합니다.

화면 켜기/끄기에 대해 Android의 브로드캐스트 수신기 `MediaPlayer` 내에서 일시 중단 및 복원 작업을 처리할 수 있습니다.

TVSDK는 조각(또는 활동)이 배경 또는 전경에 있는 시기를 확인할 수 없습니다. 또한 Android는 장치 화면이 꺼져도(활동이 일시 중지됨) Android가 파괴되지 `SurfaceView` 않습니다. 그러나 장치가 응용 프로그램을 백그라운드로 배치하면 `SurfaceView` 파괴되지 *않습니다* . TVSDK는 이러한 변경 사항을 감지할 수 없으므로 애플리케이션에서 처리해야 합니다.

다음 샘플 코드는 응용 프로그램 수준에서 장치 화면이 켜지고 꺼질 `MediaPlayer` 때 응용 프로그램에서 일시 중단 및 복원을 처리하는 방법입니다.

```java
// Track the state of a fragment to determine if it is PAUSED or RESUMED 
private boolean isActivityPaused = false; 
 
/** 
* Register the broadcast receiver to track screen on/screen off functions triggered from 
device. 
*/ 
private BroadcastReceiver mReceiver = new BroadcastReceiver() { 
    @Override 
    public void onReceive(Context context, Intent intent) { 
 
        // Call suspend when screen is turned off and mediaPlayer is not null and 
        // mediaplayer status is not suspended/Error/Released state. 
        if (intent.getAction().equals(Intent.ACTION_SCREEN_OFF)) { 
            try { 
                if (mediaPlayer != null && 
                  lastKnownStatus != MediaPlayerStatus.ERROR && 
                  lastKnownStatus != MediaPlayerStatus.RELEASED && 
                  lastKnownStatus != MediaPlayerStatus.SUSPENDED) { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOff:", 
                    "Suspending mediaplayer as screen is turned off and mediaPlayer 
                    status is " + lastKnownStatus.toString()); 
                    mediaPlayer.suspend(); 
                } 
                else { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOff:", 
                      "Not suspending mediaplayer since mediaplayer status is " 
                      + lastKnownStatus.toString()); 
                } 
            } catch(MediaPlayerException e) { 
                PrimetimeReference.logger.e(LOG_TAG+"#screenOff:", 
                  "MediaPlayer Exception for suspend() call"); 
            } 
        } 
        else if (intent.getAction().equals(Intent.ACTION_SCREEN_ON)) { 
            // Call restore when the screen is turned on and mediaplayer is not in the  
            // suspended status.  This is for the screen on condition when the device  
            // does not have a lock and turning on the screen immediately brings the  
            // fragment to the foreground. 
            try { 
                if(lastKnownStatus == MediaPlayerStatus.SUSPENDED && !isActivityPaused) { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOn:", 
                      "Restoring mediaplayer since screen is turned on and mediaPlayer status is " 
                      + lastKnownStatus.toString()); 
                    mediaPlayer.restore(); 
                } 
                else { 
                    PrimetimeReference.logger.i(LOG_TAG+"#screenOn:", 
                      "Not restoring mediaplayer since mediaPlayer status is " 
                      + lastKnownStatus.toString()); 
                } 
            } catch(MediaPlayerException e) { 
                PrimetimeReference.logger.e(LOG_TAG+"#screenOn:", 
                  "MediaPlayer Exception for restore() call"); 
            } 
        } 
    } 
}; 
 
/* 
* Activity or Fragment's onPause() overridden method 
*/ 
@Override 
public void onPause() { 
    PrimetimeReference.logger.i(LOG_TAG + "#onPause", "Player activity paused."); 
 
    // Set the fragment paused status to true when app goes in background. 
    isActivityPaused = true; 
    super.onPause(); 
} 
 
/* 
* Activity or Fragment's onResume() overridden method 
*/ 
@Override 
public void onResume() { 
    super.onResume(); 
 
    /** 
    * When the device has a lock/pin the on resume will be called only after the device 
      is unlocked. 
    * Screen on does not call the onResume() method so we need to handle restore here 
      explicitly. 
    */ 
    if(lastKnownStatus == MediaPlayerStatus.SUSPENDED && isActivityPaused) { 
        try { 
            PrimetimeReference.logger.i(LOG_TAG + "#onResume", 
              "Player restored as activity operations are resumed"); 
            mediaPlayer.restore(); 
        } 
        catch(MediaPlayerException e) { 
            PrimetimeReference.logger.i(LOG_TAG + "#onResume",  
              "Exception occured while restoring mediaPlayer"); 
        } 
    } 
    // Set the fragment paused status to false when app comes in foreground. 
    isActivityPaused = false; 
} 
```
