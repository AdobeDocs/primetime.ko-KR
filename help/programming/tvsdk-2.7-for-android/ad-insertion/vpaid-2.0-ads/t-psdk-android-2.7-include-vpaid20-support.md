---
description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가합니다.
title: VPAID 2.0 통합 구현
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# VPAID 2.0 통합 구현 {#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가합니다.

VPAID 2.0 지원을 추가하려면:

1. 플레이어가 준비됨 상태일 때 플레이어 인터페이스에 사용자 지정 광고 보기를 추가합니다.

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

1. 리스너를 만들고 이벤트 리스너에 설명된 이벤트를 처리합니다.

   >[!IMPORTANT]
   >
   >VPAID 2.0 워크플로우에서 사용자 지정 광고 보기의 경우 를 유지 관리하는 것이 매우 중요합니다. `CustomAdView` 인스턴스 가로 `AdBreak` 시작(이벤트 `AD_BREAK_START`) 및 `AdBreak` 완료(이벤트 `AD_BREAK_COMPLETE`) 사용자 지정 광고 보기를 만들 때부터 삭제할 때까지 계속합니다. 즉, 모든 광고 브레이크 시작 시 사용자 지정 광고 보기를 만들지 않고 모든 광고 브레이크 완료 시 삭제하지 마십시오.
   >
   >
   >또한 플레이어가 준비됨 상태일 때만 사용자 지정 광고 보기를 만들어야 합니다.
   >
   >
   >재설정이 호출될 때만 사용자 지정 광고 보기를 삭제합니다. 예:
   >
   >```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >```
   >
   >마지막으로, 사용자 지정 광고 보기를 삭제하기 전에 `FrameLayout`. 예:
   >
   >```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
