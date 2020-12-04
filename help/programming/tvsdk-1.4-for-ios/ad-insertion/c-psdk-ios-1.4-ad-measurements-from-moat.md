---
description: TVSDK는 FreeWheel과 다양한 서버에서 VAST 응답을 제공합니다. FreeWheel은 VAST 응답 내에서 해자 서비스에서 정보를 제공합니다. 해자 서비스는 크리에이티브가 고객의 관심사를 캡처 또는 무시함을 더 잘 보여주는 정확성을 통해 광고 노출 횟수를 계산합니다.
seo-description: TVSDK는 FreeWheel과 다양한 서버에서 VAST 응답을 제공합니다. FreeWheel은 VAST 응답 내에서 해자 서비스에서 정보를 제공합니다. 해자 서비스는 크리에이티브가 고객의 관심사를 캡처 또는 무시함을 더 잘 보여주는 정확성을 통해 광고 노출 횟수를 계산합니다.
seo-title: 해자에서 광고 측정
title: 해자에서 광고 측정
uuid: 76fa9ca0-58bd-44fe-82ce-72fdf6fcc28c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 해자{#ad-measurements-from-moat}의 광고 측정

TVSDK는 FreeWheel과 다양한 서버에서 VAST 응답을 제공합니다. FreeWheel은 VAST 응답 내에서 해자 서비스에서 정보를 제공합니다. 해자 서비스는 크리에이티브가 고객의 관심사를 캡처 또는 무시함을 더 잘 보여주는 정확성을 통해 광고 노출 횟수를 계산합니다.

해자는 브라우저에서부터 응용 프로그램 내의 다양한 용도에 걸쳐 측정하고 보는 서비스입니다. 해자는 다양한 플랫폼에서 마케팅 분석 데이터를 실시간으로 생성합니다.

VAST 응답 XML에는 속성 및 코드가 읽을 수 있는 요소, 가장 바깥쪽 광고 id 속성 및 가장 바깥쪽 확장 요소가 있습니다. 어느 방법으로든, 귀하의 코드는 TVSDK를 사용하여 광고 ID 정보와 확장 정보를 모두 저장하고 트리 구조로 정보를 구성할 수 있습니다. 이 조직을 사용하면 모든 수준에서 데이터를 수집하여 필요한 곳에 전달할 수 있습니다. 가장 바깥쪽 광고 ID 속성 값을 사용하면 코드가 연관된 캠페인의 정보를 조정할 수 있습니다.

예를 들어 FreeWheel은 Extensions 요소의 데이터를 반환할 수 있습니다. 다음은 샘플 요소입니다.

```xml
<Extensions> 
   <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
     <MeasurementInfo renditionID="6398737" type="MediaFile"> 
      <MoatID> 
       <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
       <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID> 
        <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
        <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions>
```

또한 자유 바퀴는 아래 샘플에서와 같이 광고 요소에서 id 속성을 설정할 수도 있습니다.

```
<Ad id="118566" sequence="1">
```

`PTAdAsset`의 `PTNetworkAdInfo` 클래스에 대한 API 설명서를 참조하십시오.
