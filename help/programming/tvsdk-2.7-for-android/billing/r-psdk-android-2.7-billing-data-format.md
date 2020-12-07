---
description: TVSDK는 청구 지표를 XML 형식으로 Adobe으로 전송합니다.
seo-description: TVSDK는 청구 지표를 XML 형식으로 Adobe으로 전송합니다.
seo-title: 결제 지표 전송
title: 결제 지표 전송
uuid: f4a7f50e-f457-434e-bf26-1e06cb15a038
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 청구 지표 전송 {#transmit-billing-metrics}

TVSDK는 청구 지표를 XML 형식으로 Adobe으로 전송합니다.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

네트워크 캡처 도구를 사용하여 TVSDK가 Adobe으로 전송되는 통계를 모니터하는 경우 다음과 같은 단위가 표시됩니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

부울 속성 `drmProtected`, `adsEnabled` 및 `midrollEnabled`은 true인 경우에만 나타납니다.