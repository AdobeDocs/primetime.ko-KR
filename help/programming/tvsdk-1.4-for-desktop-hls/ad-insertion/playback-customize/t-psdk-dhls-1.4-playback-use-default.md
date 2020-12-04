---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-title: 기본 재생 동작 사용
title: 기본 재생 동작 사용
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 기본 재생 동작 사용{#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

기본 동작을 사용하려면:

* 자신의 `ContentFactory` 클래스를 구현하는 경우 `doRetrieveAdPolicySelector` 구현에서 `DefaultAdPolicySelector`의 새 인스턴스를 반환합니다.

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

* `ContentFactory` 클래스에 대한 사용자 지정 구현이 없는 경우 TVSDK는 `DefaultAdPolicySelector`을 사용합니다.