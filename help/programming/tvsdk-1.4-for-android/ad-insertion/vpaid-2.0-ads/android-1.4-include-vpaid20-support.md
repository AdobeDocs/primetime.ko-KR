---
description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.
seo-description: VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.
seo-title: VPAID 2.0 통합 구현
title: VPAID 2.0 통합 구현
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# VPAID 2.0 통합 구현{#implement-vpaid-integration}

VPAID 2.0 지원을 추가하려면 사용자 지정 광고 보기와 적절한 수신기를 추가하십시오.

VPAID 2.0 지원을 추가하려면:

1. 플레이어 인터페이스에 사용자 지정 광고 보기를 추가합니다.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 사용자 지정 광고 이벤트에 대한 리스너를 추가합니다.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

