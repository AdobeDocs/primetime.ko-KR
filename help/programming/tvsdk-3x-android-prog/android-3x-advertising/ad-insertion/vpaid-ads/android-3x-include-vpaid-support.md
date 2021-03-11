---
description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 리스너를 추가하십시오.
title: VPAID 2.0 통합 구현
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# VPAID 2.0 통합 구현 {#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 리스너를 추가하십시오.

1. 플레이어가 준비 상태일 때 플레이어 인터페이스에 사용자 지정 광고 보기를 추가합니다.

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

1. 리스너를 만들고 [이벤트](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md)에 설명된 이벤트를 처리합니다.

   >[!IMPORTANT]
   >
   >VPAID 2.0 작업 과정에서 사용자 지정 광고 보기의 경우 사용자 지정 광고 보기를 만들 때부터 삭제할 때까지 `AdBreak` 시작(이벤트 `AD_BREAK_START`) 및 `AdBreak` 완료(이벤트 `AD_BREAK_COMPLETE`)에 대해 `CustomAdView` 인스턴스를 유지하는 것이 매우 중요합니다. 즉, 모든 광고 중단 시작 부분에 사용자 지정 광고 보기를 만들지 않고 전체 광고 나누기에 대해 이를 처리하지 마십시오.
   >
   >
   >또한 플레이어가 준비 상태인 경우에만 사용자 지정 광고 보기를 만들어야 합니다.
   >
   >
   >재설정이 호출될 때만 사용자 지정 광고 보기를 삭제합니다. 예:
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
   >마지막으로 사용자 지정 광고 보기를 처분하기 전에 `FrameLayout`에서 제거해야 합니다. 예:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
