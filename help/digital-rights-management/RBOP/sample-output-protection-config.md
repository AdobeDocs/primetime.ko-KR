---
description: 이 섹션에서는 구성의 개념과 형식을 보여주는 샘플 구성을 보여 줍니다.
seo-description: 이 섹션에서는 구성의 개념과 형식을 보여주는 샘플 구성을 보여 줍니다.
seo-title: 샘플 RBOP 구성
title: 샘플 RBOP 구성
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 샘플 RBOP 구성 {#sample-rbop-configuration}

이 섹션에서는 구성의 개념과 형식을 보여주는 샘플 구성을 보여 줍니다.

다음 샘플 JSON 구성은 다음을 지정하는 픽셀 출력 정책을 정의합니다.

* 비디오의 암호 해독을 1080 이하의 해상도로 제한
* 720 및 480의 해상도에 대해 특정 제한 사항을 적용합니다.

   * 720 해상도의 경우:디지털 출력을 위한 HDCP 필요;복사 *생성 관리 시스템 필요 - 아날로그* 출력을 위한 아날로그(CGMS-A) 보호
   * 480 해상도:디지털 출력을 위한 HDCP 필요;아날로그 보호 필요 없음

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

위의 샘플 구성에 대해서는 다음 사항을 참고하십시오.

* 사양은 `pixelCount` JSON 구조의 섹션 내에서 한 수준 아래에 `pixelConstraints` 있습니다.

* 각 픽셀 수 사양 내에서 디지털 출력 및 아날로그 출력 모두에 대해 출력 보호가 지정됩니다.
* 디지털 출력 사양에서는 클라이언트가 현재 HDCP 버전 지정을 지원하지 않지만 HDCP 버전이 지정됩니다. 자세한 내용은 FAQ를 참조하십시오.

