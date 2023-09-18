---
description: 기본 구성을 사용하는 경우 결제를 활성화하거나 구성하는 데 필요한 다른 작업은 없습니다. Adobe 지원 담당자로부터 다른 구성 매개 변수를 얻은 경우 미디어 플레이어를 초기화하기 전에 BillingMetricsConfiguration 클래스를 사용하여 이러한 매개 변수를 설정하십시오.
title: 청구 지표 구성
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 청구 지표 구성 {#configure-billing-metrics}

기본 구성을 사용하는 경우 결제를 활성화하거나 구성하는 데 필요한 다른 작업은 없습니다. Adobe 지원 담당자로부터 다른 구성 매개 변수를 얻은 경우 미디어 플레이어를 초기화하기 전에 BillingMetricsConfiguration 클래스를 사용하여 이러한 매개 변수를 설정하십시오.

>[!TIP]
>
>대부분의 고객은 기본 구성을 사용해야 합니다.

>[!IMPORTANT]
>
>설정한 구성은 미디어 플레이어의 수명 동안 유효합니다. 미디어 플레이어를 초기화하면 구성을 변경할 수 없습니다.

청구 지표를 구성하려면 다음 작업을 수행하십시오.

1. 다음 코드 샘플을 입력합니다.

   ```java
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
   billingConfig.setEnabled(true); 
   billingConfig.setProVODBillableDurationMinutes(60); 
   billingConfig.setStdVODBillableDurationMinutes(30); 
   billingConfig.setLiveBillableDurationMinutes(15); 
   config.setBillingMetricsConfiguration(billingConfig); 
   mediaPlayer.replaceCurrentResource(mediaResource, config);
   ```
