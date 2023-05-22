---
description: 기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.
title: 기본 재생 동작 사용
exl-id: eb4ce0b4-9dfd-4de8-8cbf-8aba093a5ddd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 기본 재생 동작 사용  {#use-the-default-playback-behavior}

기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.

1. 기본 동작을 사용하려면 다음 작업 중 하나를 완료하십시오.

   * 자체 를 구현하는 경우 `AdvertisingFactory` class, 다음에 대해 null 반환: `createAdPolicySelector`.

   * 에 대한 사용자 지정 구현이 없는 경우 `AdvertisingFactory` 클래스, TVSDK는 기본 광고 정책 선택기를 사용합니다.

## 사용자 지정 재생 설정 {#set-up-customized-playback}

광고 비헤이비어를 사용자 정의하거나 재정의할 수 있습니다.

광고 동작을 사용자 정의하거나 재정의하기 전에 TVSDK에서 광고 정책 인스턴스를 등록합니다.

* 구현 `AdPolicySelector` 인터페이스 및 모든 해당 메서드.

   재정의해야 하는 경우 이 옵션을 권장합니다. **모두** 기본 광고 동작입니다.

* 확장 `DefaultAdPolicySelector` 클래스를 만들고 맞춤화가 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 재정의해야 하는 경우에만 권장됩니다. **일부** 기본 동작.

광고 비헤이비어를 사용자 지정하려면:

1. 구현 `AdPolicySelector` 인터페이스 및 모든 해당 메서드를 사용합니다.
1. Advertising Factory를 통해 TVSDK에서 사용할 정책 인스턴스를 할당합니다.

   >[!NOTE]
   >
   >재생 시작 시 등록된 사용자 지정 광고 정책은 `MediaPlayer` 인스턴스가 할당 해제되었습니다. 애플리케이션은 새 재생 세션이 생성될 때마다 정책 선택기 인스턴스를 등록해야 합니다.

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

1. 맞춤화 구현.
