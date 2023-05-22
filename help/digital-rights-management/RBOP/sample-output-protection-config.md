---
description: 이 섹션에서는 구성의 개념 및 형식을 보여 주는 샘플 구성을 제공합니다.
title: 샘플 RBOP 구성
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 샘플 RBOP 구성 {#sample-rbop-configuration}

이 섹션에서는 구성의 개념 및 형식을 보여 주는 샘플 구성을 제공합니다.

다음 샘플 JSON 구성은 다음을 지정하는 픽셀 출력 정책을 정의합니다.

* 비디오의 암호 해독을 1080 이하의 해상도로 제한합니다.
* 해상도 720 및 480에 대해 특정 제한 적용:

   * 720 해상도의 경우: 디지털 출력을 위해 HDCP 필요, 필요 *Copy Generation Management 시스템 - 아날로그* (CGMS-A) 아날로그 출력 보호
   * 480 해상도의 경우: 디지털 출력을 위해 HDCP가 필요하며 아날로그에 대한 보호가 필요하지 않음

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

위의 샘플 구성에 대해서는 다음을 참고하십시오.

* 다음 `pixelCount` 사양은 JSON 구조에서 한 수준 아래에 있으며 `pixelConstraints` 섹션.

* 각 픽셀 카운트 사양에서, 출력 보호는 디지털 및 아날로그 출력 모두에 대해 지정된다.
* 디지털 출력 사양에서는 클라이언트가 현재 HDCP 버전 관리를 지원하지 않지만 HDCP 버전이 지정됩니다. 자세한 내용은 FAQ 를 참조하십시오.
