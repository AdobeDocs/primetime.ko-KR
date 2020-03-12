---
description: 기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 다른 작업이 필요하지 않습니다. Adobe Enablement 담당자로부터 다른 구성 매개 변수를 받은 경우 BillingMetricsConfiguration 클래스를 사용하여 미디어 플레이어를 초기화하기 전에 이러한 매개 변수를 설정하십시오.
seo-description: 기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 다른 작업이 필요하지 않습니다. Adobe Enablement 담당자로부터 다른 구성 매개 변수를 받은 경우 BillingMetricsConfiguration 클래스를 사용하여 미디어 플레이어를 초기화하기 전에 이러한 매개 변수를 설정하십시오.
seo-title: 청구 지표 구성
title: 청구 지표 구성
uuid: 04d3b53e-f08c-49d0-ba42-5375f1307d2e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 청구 지표 구성{#configure-billing-metrics}

기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 다른 작업이 필요하지 않습니다. Adobe Enablement 담당자로부터 다른 구성 매개 변수를 받은 경우 BillingMetricsConfiguration 클래스를 사용하여 미디어 플레이어를 초기화하기 전에 이러한 매개 변수를 설정하십시오.

대부분의 고객은 기본 구성을 사용해야 합니다.

>[!IMPORTANT]
>
>설정한 구성은 미디어 플레이어의 수명 동안 그대로 유지됩니다. 미디어 플레이어를 초기화한 후에는 구성을 변경할 수 없습니다.

청구 지표를 구성하려면:

* 다음 코드 샘플을 입력합니다.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   여기서 `_player` 는 의 `AdobePSDK.MediaPlayer` 인스턴스이며, `_resource` 는 의 인스턴스입니다 `AdobePSDK.MediaResource`.

