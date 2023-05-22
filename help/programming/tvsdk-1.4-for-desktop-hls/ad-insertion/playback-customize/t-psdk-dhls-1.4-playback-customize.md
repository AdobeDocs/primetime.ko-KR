---
description: 광고 비헤이비어를 사용자 정의하거나 재정의할 수 있습니다.
title: 사용자 지정 재생 설정
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 사용자 지정 재생 설정{#set-up-customized-playback}

광고 비헤이비어를 사용자 정의하거나 재정의할 수 있습니다.

광고 동작을 사용자 정의하거나 재정의하려면 먼저 광고 정책 인스턴스를( )에 등록합니다.
광고 동작을 사용자 지정하려면 다음 중 하나를 수행하십시오.

* 구현 `AdPolicySelector` 인터페이스 및 모든 해당 메서드.

   재정의해야 하는 경우 이 옵션을 권장합니다. **모두** 기본 광고 동작입니다.

* 확장 `DefaultAdPolicySelector` 클래스를 만들고 맞춤화가 필요한 비헤이비어에 대해서만 구현을 제공합니다.

   이 옵션은 재정의해야 하는 경우에만 권장됩니다. **일부** 기본 동작.

두 옵션 모두 다음 작업을 완료하십시오.

1. 사용자 지정 광고 정책 선택기를 구현합니다.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. 콘텐츠 팩토리를 확장하여 사용자 지정 광고 정책 선택기를 사용합니다.

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

1. TVSDK에서 사용할 새 콘텐츠 팩토리를 광고 워크플로에 등록합니다.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >사용자 지정 콘텐츠 팩토리가 `MediaPlayerItemConfig` 클래스, 이(가) `MediaPlayer` 인스턴스가 할당 해제되었습니다. 새 재생 세션이 생성될 때마다 애플리케이션이 이를 등록해야 합니다.
