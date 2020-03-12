---
description: 기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 다른 작업이 필요하지 않습니다. Adobe Enablement 담당자로부터 다른 구성 매개 변수를 받은 경우 BillingMetricsConfiguration 클래스를 사용하여 미디어 플레이어를 초기화하기 전에 이러한 매개 변수를 설정하십시오.
seo-description: 기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 다른 작업이 필요하지 않습니다. Adobe Enablement 담당자로부터 다른 구성 매개 변수를 받은 경우 BillingMetricsConfiguration 클래스를 사용하여 미디어 플레이어를 초기화하기 전에 이러한 매개 변수를 설정하십시오.
seo-title: 청구 지표 구성
title: 청구 지표 구성
uuid: 340439bf-185b-4761-a481-010908842811
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 청구 지표 구성 {#configure-billing-metrics}

기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 다른 작업이 필요하지 않습니다. Adobe Enablement 담당자로부터 다른 구성 매개 변수를 받은 경우 BillingMetricsConfiguration 클래스를 사용하여 미디어 플레이어를 초기화하기 전에 이러한 매개 변수를 설정하십시오.

>[!TIP]
>
>대부분의 고객은 기본 구성을 사용해야 합니다.

>[!IMPORTANT]
>
>설정한 구성은 미디어 플레이어의 수명 동안 그대로 유지됩니다. 미디어 플레이어를 초기화한 후에는 구성을 변경할 수 없습니다.

청구 지표를 구성하려면:

다음 코드 샘플을 입력합니다.

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
