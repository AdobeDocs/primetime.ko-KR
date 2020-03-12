---
description: Browser TVSDK는 XML 형식으로 빌링 지표를 Adobe에 전송합니다.
seo-description: Browser TVSDK는 XML 형식으로 빌링 지표를 Adobe에 전송합니다.
seo-title: 청구 지표 전송
title: 청구 지표 전송
uuid: ed2638d2-7894-4840-b31a-51e48e0a3f49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 청구 지표 전송{#transmit-billing-metrics}

Browser TVSDK는 XML 형식으로 빌링 지표를 Adobe에 전송합니다.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

네트워크 캡처 도구를 사용하여 통계를 모니터하는 경우 브라우저 TVSDK가 Adobe로 전송되면 다음과 같은 장치가 표시됩니다.

```
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