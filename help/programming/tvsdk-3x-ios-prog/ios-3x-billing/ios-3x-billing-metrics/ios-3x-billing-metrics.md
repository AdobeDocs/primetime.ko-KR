---
description: 실제 사용과 상관없이 고정 요금이 아니라 사용하는 만큼만 지불하고자 하는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이 지표를 사용하여 고객에게 청구할 금액을 결정합니다.
title: 청구 사용 지표
exl-id: 8b76d8ea-c8d6-427b-886a-4ae8764bd47a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 청구 지표 {#billing-metrics}

실제 사용과 상관없이 고정 요금이 아니라 사용하는 만큼만 지불하고자 하는 고객을 수용하기 위해 Adobe은 사용 지표를 수집하고 이 지표를 사용하여 고객에게 청구할 금액을 결정합니다.

플레이어가 스트림 시작 이벤트를 생성할 때마다 TVSDK는 주기적으로 HTTP 메시지를 Adobe의 과금 시스템으로 전송하기 시작합니다. 청구 가능 기간이라고 하는 기간은 표준 VOD, 프로 VOD(미드롤 광고 활성화) 및 라이브 컨텐츠에 대해 다를 수 있습니다. 각 컨텐츠 유형의 기본 기간은 30분이지만 Adobe과의 계약에 따라 실제 값이 결정됩니다.

메시지에는 다음 정보가 포함됩니다.

* 컨텐츠 유형(라이브, 선형 또는 VOD)
* 컨텐츠 URL
* 광고가 활성화되었는지 여부
* 미드롤 광고 활성화 여부(VOD만 해당)
* 스트림이 DRM으로 보호되는지 여부
* TVSDK 버전 및 플랫폼

Adobe은 이 배열을 미리 구성하지만 배열을 변경하려면 Adobe 지원 담당자와 협력합니다.

TVSDK가 Adobe에 보내는 통계를 모니터링하려면 Adobe 지원 담당자로부터 URL을 가져온 다음, 네트워크 캡처 도구(예: Charles)를 사용하여 데이터를 봅니다.

## 청구 지표 구성 {#configure-billing-metrics}

기본 구성을 사용하는 경우 결제를 활성화하거나 구성하는 데 필요한 다른 작업은 없습니다. Adobe 지원 담당자로부터 다른 구성 매개 변수를 얻은 경우 미디어 플레이어를 초기화하기 전에 PTBillingMetricsConfiguration 클래스를 사용하여 이러한 매개 변수를 설정하십시오.

대부분의 고객은 기본 구성을 사용해야 합니다.

>[!IMPORTANT]
>
>설정한 구성은 미디어 플레이어의 수명 동안 유효합니다. 미디어 플레이어를 초기화하면 구성을 변경할 수 없습니다.

청구 지표를 구성하려면 다음 작업을 수행하십시오.

다음 코드 샘플을 입력합니다.

```
PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
billingConfig.enabled = YES; 
billingConfig.stdVODBillableDurationMinutes = 60.0; 
billingConfig.proVODBillableDurationMinutes = 30.0; 
billingConfig.liveBillableDurationMinutes = 15.0; 
                
// metadata is the PTMetadata instance set on PTMediaPlayerItem 
[metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
```

## 과금 지표 전송 {#transmit-billing-metrics}

TVSDK가 청구 지표를 XML 형식으로 Adobe에 보냅니다.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

네트워크 캡처 도구를 사용하여 TVSDK가 Adobe에 전송하는 통계를 모니터링하는 경우 다음과 같은 단위가 표시됩니다.

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

부울 속성 `drmProtected`, `adsEnabled`, 및 `midrollEnabled` true인 경우에만 표시됩니다.
