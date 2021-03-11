---
description: 실제 사용과 상관없이 고정 요금 대신 자신이 사용하는 것에 대해서만 비용을 지불하려는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이러한 지표를 사용하여 고객에게 청구할 비용을 결정합니다.
title: 청구 지표
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# 청구 지표 {#billing-metrics}

실제 사용과 상관없이 고정 요금 대신 자신이 사용하는 것에 대해서만 비용을 지불하려는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이러한 지표를 사용하여 고객에게 청구할 비용을 결정합니다.

플레이어가 스트림 시작 이벤트를 생성할 때마다 TVSDK는 HTTP 메시지를 Adobe의 결제 시스템으로 주기적으로 보내기 시작합니다. 청구 가능한 기간이라고 하는 기간은 표준 VOD, 프로 VOD(중간 롤 광고 활성화) 및 라이브 컨텐츠에 대해 다를 수 있습니다. 각 컨텐츠 유형의 기본 기간은 30분이지만 Adobe과의 계약에 따라 실제 값이 결정됩니다.

메시지에는 다음 정보가 포함되어 있습니다.

* 컨텐츠 유형(실시간, 선형 또는 VOD)
* 콘텐트 URL
* 광고 활성화 여부
* 미드롤 광고를 활성화할지 여부(VOD만 해당)
* 스트림이 DRM으로 보호되는지 여부
* TVSDK 버전 및 플랫폼

Adobe은 이러한 배열을 미리 구성하지만, 배열을 변경하려면 Adobe 지원 담당자에게 문의하십시오.

TVSDK가 Adobe으로 보내는 통계를 모니터링하려면 Adobe 활성화 담당자의 URL을 입수하고 네트워크 캡처 도구(예: Charles)를 사용하여 데이터를 확인합니다.

## 청구 지표 구성 {#configure-billing-metrics}

기본 구성을 사용하는 경우 청구를 활성화하거나 구성하는 데 필요한 다른 작업은 없습니다. Adobe 활성화 담당자로부터 다른 구성 매개 변수를 받은 경우 미디어 플레이어를 초기화하기 전에 PTBlingMetricsConfiguration 클래스를 사용하여 이러한 매개 변수를 설정하십시오.

대부분의 고객은 기본 구성을 사용해야 합니다.

>[!IMPORTANT]
>
>설정한 구성은 미디어 플레이어의 수명 동안 그대로 유지됩니다. 미디어 플레이어를 초기화한 후에는 구성을 변경할 수 없습니다.

청구 지표를 구성하려면:

1. 다음 코드 샘플을 입력합니다.

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## 청구 지표 전송 {#transmit-billing-metrics}

TVSDK는 XML 포맷으로 결제 지표를 Adobe으로 보냅니다.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

네트워크 캡처 도구를 사용하여 TV SDK가 Adobe으로 전송하는 통계를 모니터링하는 경우 다음과 같은 단위가 표시됩니다.

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

부울 속성 `drmProtected`, `adsEnabled` 및 `midrollEnabled`은 true인 경우에만 나타납니다.