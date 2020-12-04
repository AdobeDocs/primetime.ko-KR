---
description: 광고 행동을 사용자 정의하거나 무시할 수 있습니다.
seo-description: 광고 행동을 사용자 정의하거나 무시할 수 있습니다.
seo-title: 사용자 정의 재생 설정
title: 사용자 정의 재생 설정
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# 사용자 지정된 재생 설정{#set-up-customized-playback}

광고 행동을 사용자 정의하거나 무시할 수 있습니다.

광고 행동을 사용자 정의하거나 무시하려면 먼저 에 광고 정책 인스턴스를 등록하십시오.
광고 동작을 사용자 정의하려면 다음 중 하나를 수행합니다.

* `AdPolicySelector` 인터페이스와 모든 메서드를 구현합니다.

   이 옵션은 기본 광고 비헤이비어를 **모두**&#x200B;로 대체해야 하는 경우 권장됩니다.

* `DefaultAdPolicySelector` 클래스를 확장하고 사용자 지정이 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 기본 비헤이비어의 **일부**&#x200B;만 재정의해야 하는 경우에 좋습니다.

두 옵션 모두에 대해 다음 작업을 완료하십시오.

1. 고유한 사용자 지정 광고 정책 선택기를 구현합니다.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. 사용자 지정 광고 정책 선택기를 사용하도록 컨텐츠 팩터리를 확장합니다.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. 광고 워크플로우에서 TVSDK에서 사용할 새로운 컨텐츠 팩터리를 등록합니다.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >사용자 지정 콘텐츠 팩터리가 `MediaPlayerItemConfig` 클래스를 통해 특정 스트림에 등록되어 있는 경우 `MediaPlayer` 인스턴스의 할당을 해제하면 지워집니다. 새로운 재생 세션이 생성될 때마다 응용 프로그램이 등록해야 합니다.