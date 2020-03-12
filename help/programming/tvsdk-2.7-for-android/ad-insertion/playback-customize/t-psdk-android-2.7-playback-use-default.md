---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-title: 기본 재생 동작 사용
title: 기본 재생 동작 사용
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

1. 기본 동작을 사용하려면 다음 작업 중 하나를 완료하십시오.

   * 고유한 `AdvertisingFactory` 클래스를 구현하는 경우 에 대해 null을 `createAdPolicySelector`반환합니다.

   * 클래스에 대한 사용자 정의 구현이 없는 경우 TVSDK는 기본 광고 정책 선택기를 사용합니다. `AdvertisingFactory`

## 사용자 정의 재생 설정 {#set-up-customized-playback}

광고 행동을 사용자 정의하거나 무시할 수 있습니다.

광고 행동을 사용자 정의하거나 무시하기 전에 광고 정책 인스턴스를 TVSDK에 등록합니다.

* 인터페이스와 모든 해당 메서드를 구현합니다. `AdPolicySelector`

   이 옵션은 **모든** 기본 광고 동작을 재정의해야 하는 경우에 권장됩니다.

* 클래스를 `DefaultAdPolicySelector` 확장하고 사용자 지정이 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 **일부** 기본 동작만 재정의해야 하는 경우에 권장됩니다.

광고 비헤이비어를 사용자 정의하려면

1. 인터페이스와 모든 해당 메서드를 구현합니다. `AdPolicySelector`
1. 광고 공장을 통해 TVSDK에서 사용할 정책 인스턴스를 지정합니다.

   >[!NOTE]
   >
   >재생 시작 시 등록된 사용자 정의 광고 정책은 `MediaPlayer` 인스턴스가 할당 해제될 때 지워집니다. 응용 프로그램은 새 재생 세션이 생성될 때마다 정책 선택기 인스턴스를 등록해야 합니다.

   예:

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. 사용자 정의 구현