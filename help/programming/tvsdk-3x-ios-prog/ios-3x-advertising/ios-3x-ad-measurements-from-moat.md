---
description: TVSDK는 다양한 응답을 제공하는 FreeWheel과 기타 adserver의 정보를 제공합니다. FreeWheel은 해자 서비스에서 얻은 정보를 VAST 응답 내에서 제공합니다. 해자 서비스는 크리에이티브가 대상자의 관심을 끌거나 방치하는 것을 보다 정확하게 보여주는 광고 노출 횟수를 카운트합니다.
title: 해자에서 광고 측정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 해자의 광고 측정 {#ad-measurements-from-moat}

TVSDK는 다양한 응답을 제공하는 FreeWheel과 기타 adserver의 정보를 제공합니다. FreeWheel은 해자 서비스에서 얻은 정보를 VAST 응답 내에서 제공합니다. 해자 서비스는 크리에이티브가 대상자의 관심을 끌거나 방치하는 것을 보다 정확하게 보여주는 광고 노출 횟수를 카운트합니다.

해자는 브라우저에서부터 응용 프로그램 내의 다양한 사용 방법을 측정하고 보는 서비스입니다. 해자는 여러 플랫폼에서 마케팅 분석 데이터를 실시간으로 생성합니다.

VAST 응답 XML에는 코드가 읽을 수 있는 속성, 가장 바깥쪽 광고 id 속성 및 가장 바깥쪽 확장 요소가 있습니다. 어떤 방식으로든 TVSDK를 사용하여 광고 ID 정보와 확장 정보를 모두 저장하고 트리 구조의 정보를 구성할 수 있습니다. 이 조직을 사용하면 모든 수준에서 데이터를 수집하여 필요한 곳에 전달할 수 있습니다. 가장 바깥쪽 광고 id 속성 값을 사용하면 코드가 연관된 캠페인의 정보를 조정할 수 있습니다.

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

또한 자유 바퀴는 아래 샘플에서와 같이 광고 요소에 id 속성을 설정할 수도 있습니다.

```
<Ad id="118566" sequence="1">
```

`PTAdAsset`의 `PTNetworkAdInfo` 클래스에 대한 API 설명서를 참조하십시오.