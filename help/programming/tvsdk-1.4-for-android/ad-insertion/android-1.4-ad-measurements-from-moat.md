---
description: TVSDK는 FreeWheel 및 VAST 응답을 제공하는 기타 광고 서버에서 정보를 가져옵니다. FreeWheel은 VAST 응답 내에서 Moat 서비스에서 정보를 제공합니다. Moat 서비스는 광고 크리에이티브가 대상의 관심사를 포착하는지 또는 무시하는지를 더 잘 보여 주는 정확도로 광고 노출 횟수를 계산합니다.
title: Moat의 광고 측정
exl-id: 7ce1a495-a88f-4c96-90b1-1d30933b3dcf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Moat의 광고 측정{#ad-measurements-from-moat}

TVSDK는 FreeWheel 및 VAST 응답을 제공하는 기타 광고 서버에서 정보를 가져옵니다. FreeWheel은 VAST 응답 내에서 Moat 서비스에서 정보를 제공합니다. Moat 서비스는 광고 크리에이티브가 대상의 관심사를 포착하는지 또는 무시하는지를 더 잘 보여 주는 정확도로 광고 노출 횟수를 계산합니다.

Moat는 브라우저에서 애플리케이션 내에서까지 다양한 사용에서 광고 보기를 측정하는 서비스입니다. Moat은 여러 플랫폼에서 실시간으로 마케팅 분석 데이터를 생성합니다.

VAST 응답 XML에는 코드에서 읽을 수 있는 속성과 요소가 가장 바깥쪽에 있습니다 `Ad id` 속성 및 가장 바깥쪽 `Extension` 요소를 생성하지 않습니다. 어느 경우든지 코드에서 TVSDK를 사용하여 `Ad id` 정보 및 `Extension` 정보를 구성한 다음 트리 구조로 정보를 구성합니다. 이 조직을 사용하면 코드가 모든 수준에서 데이터를 선택하여 필요한 위치로 전달할 수 있습니다. 가장 바깥쪽의 값 `Ad id` 속성을 사용하면 코드가 연관된 캠페인의 정보를 조정할 수 있습니다.

예를 들어 FreeWheel은 확장 요소에서 데이터를 반환할 수 있습니다. 다음은 샘플 요소입니다.

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

Freewheel은 `id` 의 속성 `Ad` 아래 샘플에서와 같이 요소를 선택합니다.

```xml
<Ad id="118566" sequence="1">
```

클래스에 대한 API 설명서 를 참조하십시오 `NetworkAdInfo`.
