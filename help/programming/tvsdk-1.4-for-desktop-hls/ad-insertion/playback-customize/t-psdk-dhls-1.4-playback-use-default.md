---
description: 기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.
title: 기본 재생 동작 사용
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 기본 재생 동작 사용{#use-the-default-playback-behavior}

기본 광고 비헤이비어를 사용하도록 선택할 수 있습니다.

기본 비헤이비어를 사용하려면

* 자체 를 구현하는 경우 `ContentFactory` 클래스, 새 인스턴스 반환 `DefaultAdPolicySelector` 의 구현에서 `doRetrieveAdPolicySelector`.

  ```
  public class CustomContentFactory extends ContentFactory { 
  
      //... 
      // your custom code for advertising classes 
      //... 
  
      /** 
       * @inheritDoc 
       */ 
      override protected function  
        doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
          return new DefaultAdPolicySelector(item); 
      } 
  }
  ```

* 에 대한 사용자 지정 구현이 없는 경우 `ContentFactory` 클래스, TVSDK 사용 `DefaultAdPolicySelector`.
