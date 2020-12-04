---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-title: 기본 재생 동작 사용
title: 기본 재생 동작 사용
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 기본 재생 동작 사용 {#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

1. 기본 동작을 사용하려면 다음 작업 중 하나를 완료하십시오.

   * 자신의 `AdvertisingFactory` 클래스를 구현하는 경우 `createAdPolicySelector`에 대해 null을 반환합니다.

   * `AdvertisingFactory` 클래스에 대한 사용자 지정 구현이 없는 경우 TVSDK는 기본 광고 정책 선택기를 사용합니다.

## 사용자 지정된 재생 {#set-up-customized-playback} 설정

광고 행동을 사용자 정의하거나 무시할 수 있습니다.

광고 행동을 사용자 정의하거나 무시하기 전에 광고 정책 인스턴스를 TVSDK에 등록합니다.

* `AdPolicySelector` 인터페이스와 모든 메서드를 구현합니다.

   이 옵션은 기본 광고 비헤이비어를 **모두**&#x200B;로 대체해야 하는 경우 권장됩니다.

* `DefaultAdPolicySelector` 클래스를 확장하고 사용자 지정이 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 기본 비헤이비어의 **일부**&#x200B;만 재정의해야 하는 경우에 좋습니다.

광고 행동을 사용자 정의하려면

1. `AdPolicySelector` 인터페이스와 모든 메서드를 구현합니다.
1. 광고 공장을 통해 TVSDK에서 사용할 정책 인스턴스를 할당합니다.

   >[!NOTE]
   >
   >재생 시작 시 등록된 사용자 지정 광고 정책은 `MediaPlayer` 인스턴스가 지연될 때 지워집니다. 새 재생 세션이 생성될 때마다 응용 프로그램에서 정책 선택기 인스턴스를 등록해야 합니다.

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