---
description: 사용자가 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답해야 합니다. TVSDK는 클릭할 대상 URL에 대한 정보를 제공합니다.
title: 광고 클릭에 응답
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 광고 클릭에 응답 {#respond-to-clicks-on-ads}

TVSDK는 클릭스루 광고에 대해 작업을 수행할 수 있도록 정보를 제공합니다. 플레이어 UI를 만들 때, 사용자가 클릭 가능한 광고를 클릭할 때 응답하는 방법을 결정해야 합니다.

Android용 TVSDK의 경우 선형 광고만 클릭할 수 있습니다.
사용자가 광고 또는 관련 버튼을 클릭하면 애플리케이션이 응답해야 합니다. TVSDK는 클릭할 대상 URL에 대한 정보를 제공합니다.

1. TVSDK에 대한 이벤트 리스너를 설정하고 클릭스루 정보를 제공하려면 등록합니다 `AdClickedEventListener.onAdClicked`.

   사용자가 광고 또는 관련 버튼을 클릭하면 TVSDK가 클릭 대상에 대한 정보를 포함하여 이 알림을 발송합니다.
1. 클릭 가능한 광고에서 사용자 상호 작용을 모니터링합니다.
1. 사용자가 광고 또는 버튼을 터치하거나 클릭할 때 TVSDK에 알리려면 을 호출합니다. `notifyClick` 다음에 있음 `MediaPlayerView`.
1. 다음을 들어보십시오. `onAdClick(AdClickEvent event)` tvsdk의 이벤트입니다.
1. 클릭스루 URL 및 관련 정보를 검색하려면 `AdClickEvent` 인스턴스.
1. 비디오를 일시 중지합니다.

   비디오 일시 중지에 대한 자세한 내용은  [재생 일시 중지 및 다시 시작](../../ad-insertion/clickable-ads/android-3x-pausing-resuming-playback.md).
1. 클릭스루 정보를 사용하여 광고 클릭스루 URL 및 관련 정보를 표시합니다. 예를 들어 다음 방법 중 하나로 정보를 표시할 수 있습니다.

   * 애플리케이션에서 브라우저에서 클릭스루 URL을 열어

     데스크톱 플랫폼에서는 사용자 클릭 시 클릭스루 URL을 호출하는 데 비디오 광고 재생 영역을 사용합니다.
   * 사용자를 외부 모바일 웹 브라우저로 리디렉션합니다.

     모바일 장치에서 비디오 광고 재생 영역은 컨트롤 숨기기 및 표시, 재생 일시 중지, 전체 화면으로 확장 등의 다른 기능에 사용됩니다. 이러한 장치에서는 스폰서 버튼과 같은 별도의 보기를 사용하여 클릭스루 URL을 시작합니다.

1. 클릭스루 정보가 표시되는 브라우저 창을 닫고 비디오 재생을 재개합니다.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

예:

```java
private AdStartedEventListener adStartedEventListener =  
  new AdStartedEventListener() { 
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
 
private AdCompletedEventListener adCompletedEventListener =  
  new AdCompletedEventListener() { 
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
 
private AdClickedEventListener adClickedEventListener =  
  new AdClickedEventListener() { 
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
