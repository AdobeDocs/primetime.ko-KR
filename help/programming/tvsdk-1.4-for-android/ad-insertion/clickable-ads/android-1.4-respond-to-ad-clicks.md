---
description: 사용자가 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답해야 합니다. TVSDK 파섹
seo-description: 사용자가 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답해야 합니다. TVSDK 파섹
seo-title: 광고 클릭 수에 응답
title: 광고 클릭 수에 응답
uuid: 31852f01-c900-48e3-ae23-7fb131c22594
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 광고 클릭 수에 응답{#respond-to-clicks-on-ads}

사용자가 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답해야 합니다. TVSDK 파섹

1. TVSDK에 대한 이벤트 리스너를 설정하고 클릭스루 정보를 제공하려면 을 `AdClickedEventListener.onAdClicked`등록합니다.

   사용자가 광고 또는 관련 단추를 클릭하면 TVSDK가 클릭 대상에 대한 정보를 포함하여 이 알림을 전달합니다.
1. 클릭 가능한 광고에서 사용자 인터랙션을 모니터링할 수 있습니다.
1. 사용자가 광고 또는 단추를 터치하거나 클릭하면 TVSDK에 알리려면 `notifyClick` 을 `MediaPlayerView`호출합니다.
1. TVSDK에서 이벤트를 `onAdClick(AdClickEvent event)` 수신합니다.
1. 클릭스루 URL 및 관련 정보를 검색하려면 `AdClickEvent` 인스턴스에 대해 getter 메서드를 사용합니다.
1. 비디오를 일시 중지합니다.

   비디오 일시 중단에 대한 자세한 내용은 재생 일시 [중지 및 다시 시작을 참조하십시오.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. 클릭스루 정보를 사용하여 광고 클릭스루 URL과 관련 정보를 표시합니다.

       예를 들어 다음 방법 중 하나로 정보를 표시할 수 있습니다.
   
   * 브라우저에서 클릭스루 URL을 열어 애플리케이션에서

      데스크탑 플랫폼에서 비디오 광고 재생 영역은 클릭스루 URL을 호출할 때 사용됩니다.
   * 사용자를 외부 모바일 웹 브라우저로 리디렉션합니다.

      모바일 장치에서 비디오 광고 재생 영역은 컨트롤 숨기기 및 표시, 재생 일시 중지, 전체 화면으로 확장 등과 같은 다른 기능에 사용됩니다. 이러한 장치에서는 스폰서 버튼과 같은 별도의 보기를 사용하여 클릭스루 URL을 실행합니다.

1. 클릭스루 정보가 표시되는 브라우저 창을 닫고 비디오 재생을 다시 시작합니다.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

예:

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
 
    } 
}; 
```

