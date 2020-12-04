---
description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.
seo-description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.
seo-title: VPAID 2.0 통합 구현
title: VPAID 2.0 통합 구현
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 83df68905f74931355264661aed6cff43b802d3f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# VPAID 2.0 통합 구현 {#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.

1. 플레이어가 준비 상태일 때 사용자 지정 광고 보기를 플레이어 인터페이스에 추가합니다.

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. 수신기를 만들고 [Events](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md)에 설명된 이벤트를 처리합니다.

   >[!IMPORTANT]
   >
   >VPAID 2.0 워크플로우에서 사용자 지정 광고 보기의 경우 사용자 지정 광고 보기를 만들 때부터 삭제할 때까지 `AdBreak` 시작(event `AD_BREAK_START`) 및 `AdBreak` 완료(event `AD_BREAK_COMPLETE`)에 걸쳐 `CustomAdView` 인스턴스를 유지하는 것이 매우 중요합니다. 즉, 모든 광고 중단 시작 시 사용자 지정 광고 보기를 만들지 않고 전체 광고 중단 시 이를 처리하지 마십시오.
   >
   >
   >또한 플레이어가 준비 상태인 경우에만 사용자 지정 광고 보기를 만들어야 합니다.
   >
   >
   >재설정이 호출될 때만 사용자 지정 광고 보기가 처리됩니다. 예:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >마지막으로, 사용자 지정 광고 보기를 처분하기 전에 `FrameLayout`에서 제거해야 합니다. 예:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
