---
description: TVSDK 파섹
seo-description: TVSDK 파섹
seo-title: 청구 지표 전송
title: 청구 지표 전송
uuid: c925800c-0fb7-4781-94e8-7e7ad94bb965
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 청구 지표 전송 {#transmit-billing-metrics}

TVSDK 파섹

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

네트워크 캡처 도구를 사용하여 TVSDK가 Adobe로 전송하는 통계를 모니터링하는 경우 다음과 같은 장치가 표시됩니다.

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

부울 속성은 `drmProtected`true인 경우에만 `adsEnabled`표시되고 `midrollEnabled` 표시됩니다.