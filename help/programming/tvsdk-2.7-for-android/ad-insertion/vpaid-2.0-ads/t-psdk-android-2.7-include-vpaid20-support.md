---
description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.
seo-description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.
seo-title: VPAID 2.0 통합 구현
title: VPAID 2.0 통합 구현
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# VPAID 2.0 통합 구현 {#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.

VPAID 2.0 지원을 추가하려면:

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

1. 리스너를 만들고 이벤트 리스너에 설명된 이벤트를 처리합니다.

   >[!IMPORTANT]
   >
   >VPAID 2.0 워크플로우에서 사용자 지정 광고 보기의 경우, 사용자 지정 광고 보기를 만들 때부터 삭제할 때까지 `CustomAdView` 시작(이벤트 `AdBreak` )에 걸쳐 인스턴스를 유지하고 `AD_BREAK_START`완료(이벤트 `AdBreak` `AD_BREAK_COMPLETE`)하는 것이 매우 중요합니다. 즉, 모든 광고 중단 시작 시 사용자 지정 광고 보기를 만들지 말고, 모든 광고 전환이 완료될 때 이를 처리하지 마십시오.
   >
   >
   >또한 플레이어가 준비 상태일 때만 사용자 지정 광고 보기를 만들어야 합니다.
   >
   >
   >재설정이 호출될 때 사용자 지정 광고 보기만 삭제합니다. 예:
   >
   >```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >마지막으로 사용자 지정 광고 보기를 처분하기 전에 에서 제거해야 합니다 `FrameLayout`. 예:
   >
   >```
   >if (_playerFrame != null) 
   >   _playerFrame.removeAllViews(); 
   >```
