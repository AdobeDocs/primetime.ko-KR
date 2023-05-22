---
description: 기본 구성을 사용하는 경우 결제를 활성화하거나 구성하는 데 필요한 다른 작업은 없습니다. Adobe 지원 담당자로부터 다른 구성 매개 변수를 얻은 경우 미디어 플레이어를 초기화하기 전에 BillingMetricsConfiguration 클래스를 사용하여 이러한 매개 변수를 설정하십시오.
title: 청구 지표 구성
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 청구 지표 구성{#configure-billing-metrics}

기본 구성을 사용하는 경우 결제를 활성화하거나 구성하는 데 필요한 다른 작업은 없습니다. Adobe 지원 담당자로부터 다른 구성 매개 변수를 얻은 경우 미디어 플레이어를 초기화하기 전에 BillingMetricsConfiguration 클래스를 사용하여 이러한 매개 변수를 설정하십시오.

대부분의 고객은 기본 구성을 사용해야 합니다.

>[!IMPORTANT]
>
>설정한 구성은 미디어 플레이어의 수명 동안 유효합니다. 미디어 플레이어를 초기화하면 구성을 변경할 수 없습니다.

청구 지표를 구성하려면 다음 작업을 수행하십시오.

* 다음 코드 샘플을 입력합니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   위치 `_player` 의 인스턴스임 `AdobePSDK.MediaPlayer` 및 `_resource` 의 인스턴스임 `AdobePSDK.MediaResource`.
