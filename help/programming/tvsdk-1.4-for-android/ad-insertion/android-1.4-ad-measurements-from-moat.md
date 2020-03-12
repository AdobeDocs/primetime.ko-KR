---
description: TVSDK 파섹 FreeWheel은 VAST 응답 내에서 해자 서비스에서 정보를 제공합니다. 해자 서비스는 크리에이티브가 고객의 관심을 사로잡고 방치하는지 여부를 보다 정확하게 보여주는 정확성을 통해 광고 임프레션을 계산합니다.
seo-description: TVSDK 파섹 FreeWheel은 VAST 응답 내에서 해자 서비스에서 정보를 제공합니다. 해자 서비스는 크리에이티브가 고객의 관심을 사로잡고 방치하는지 여부를 보다 정확하게 보여주는 정확성을 통해 광고 임프레션을 계산합니다.
seo-title: 해자의 광고 측정
title: 해자의 광고 측정
uuid: 73ef3a14-7ad6-4e67-8ad3-eabbeb898a09
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 해자의 광고 측정{#ad-measurements-from-moat}

TVSDK 파섹 FreeWheel은 VAST 응답 내에서 해자 서비스에서 정보를 제공합니다. 해자 서비스는 크리에이티브가 고객의 관심을 사로잡고 방치하는지 여부를 보다 정확하게 보여주는 정확성을 통해 광고 임프레션을 계산합니다.

해자는 브라우저에서부터 응용 프로그램 내에서 다양한 용도로 측정 및 보는 서비스입니다. 해자는 마케팅 분석 데이터를 여러 플랫폼에서 실시간으로 생성합니다.

VAST 응답 XML에는 코드가 읽을 수 있는 속성, 가장 바깥쪽 `Ad id` 속성 및 가장 바깥쪽 `Extension` 요소가 있습니다. 어떤 방식으로든, 코드에서는 TVSDK를 사용하여 `Ad id` 정보와 `Extension` 정보를 모두 저장한 다음 트리 구조로 정보를 구성할 수 있습니다. 이 조직을 사용하면 모든 수준에서 데이터를 수집하여 필요한 곳에 전달할 수 있습니다. 가장 바깥쪽 `Ad id` 속성 값을 사용하면 코드가 연결된 캠페인의 정보를 조정할 수 있습니다.

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

또한 Freewheel은 아래 샘플에서와 같이 `id` `Ad` 요소의 속성을 설정할 수 있습니다.

```xml
<Ad id="118566" sequence="1">
```

클래스에 대한 API 설명서를 참조하십시오 `NetworkAdInfo`.
