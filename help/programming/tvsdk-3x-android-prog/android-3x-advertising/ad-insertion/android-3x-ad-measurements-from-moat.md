---
description: TVSDK는 다양한 응답을 제공하는 FreeWheel 및 기타 광고 서버의 정보를 받습니다. FreeWheel은 해자 서비스에서 얻은 정보를 VAST 응답 내에서 제공합니다. 해자 서비스는 크리에이티브가 대상자의 관심을 끌거나 무시하는지를 보다 정확하게 보여줄 수 있도록 광고 노출 횟수를 카운트합니다.
title: 해자에서 광고 측정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# 해자의 광고 측정 {#ad-measurements-from-moat}

TVSDK는 다양한 응답을 제공하는 FreeWheel 및 기타 광고 서버의 정보를 받습니다. FreeWheel은 해자 서비스에서 얻은 정보를 VAST 응답 내에서 제공합니다. 해자 서비스는 크리에이티브가 대상자의 관심을 끌거나 무시하는지를 보다 정확하게 보여줄 수 있도록 광고 노출 횟수를 카운트합니다.

해자는 브라우저에서부터 응용 프로그램 내의 다양한 사용 방법을 측정하고 보는 서비스입니다. 해자는 여러 플랫폼에서 마케팅 분석 데이터를 실시간으로 생성합니다.

VAST 응답 XML에는 속성 및 코드가 읽을 수 있는 요소, 가장 바깥쪽 `Ad id` 속성 및 가장 바깥쪽 `Extension` 요소가 있습니다. 어떤 방식으로든 코드에서는 TVSDK를 사용하여 `Ad id` 정보와 `Extension` 정보를 모두 저장한 다음 트리 구조로 정보를 구성할 수 있습니다. 이 조직을 사용하면 모든 수준에서 데이터를 수집하여 필요한 곳에 전달할 수 있습니다. 가장 바깥쪽 `Ad id` 속성 값을 사용하면 코드가 연관된 캠페인의 정보를 조정할 수 있습니다.

예를 들어 FreeWheel은 Extensions 요소의 데이터를 반환할 수 있습니다. 다음은 샘플 요소입니다.

```xml
<?xml version="1.0"?> 
<Extensions> 
  <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
      <MeasurementInfo renditionID="6398737" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions> 
```

또한 자유형 바퀴는 아래 샘플에서와 같이 `Ad` 요소에서 `id` 속성을 설정할 수도 있습니다.

```xml
<Ad id="118566" sequence="1">
```

API 정보는 `NetworkAdInfo` 클래스에 대한 API 설명서를 참조하십시오.