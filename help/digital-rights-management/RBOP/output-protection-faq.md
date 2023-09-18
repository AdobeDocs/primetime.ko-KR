---
description: 해상도 기반 출력 보호 사용에 대한 FAQ입니다.
title: RBOP FAQ
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# RBOP FAQ {#rbop-faq}

해상도 기반 출력 보호 사용에 대한 FAQ입니다.

* **질문.** *픽셀 제한에 대한 디지털 출력 요구 사항을 정의할 때 HDCP 버전을 제외한 상태에서 구문 분석/서식 오류가 발생하지만 HDCP 요구 사항이 없습니다. 이 경우 디지털 출력 요구 사항을 어떻게 구성해야 합니까?* **A.** Adobe 현재 클라이언트에서는 HDCP 버전 확인이 지원되지 않으므로 HDCP 버전을 로 설정하는 것이 좋습니다. `1.0`. 이렇게 하면 HDCP 버전 검사가 지원될 때 구성이 올바르게 포맷되고 차후에 의미상 일관성을 유지합니다. 다음 코드 조각은 이 HDCP 값을 사용하는 구성을 보여 줍니다.

  ```
  { "pixelConstraints":  
    [  
      { "pixelCount": 720, "digital":  
        [  
          {  
            "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
          }  
        ]  
      }  
    ]  
  }
  ```

* **질문.** *RBOP 픽셀 제약은 이산적입니까, 아니면 범위를 기반으로 합니까?* **A.** RBOP 픽셀 제약은 범위를 기반으로 합니다. 각 픽셀 카운트는 주어진 카운트 이하의 모든 픽셀 카운트 또는 두 개 이상의 픽셀 구속이 존재하는 경우 해당 값보다 작은 최대 카운트까지의 요구 사항을 정의합니다. 간단히 말해서, 값들은 각각의 수직 픽셀 카운트에 대한 최대 임계값들로서 적용된다.

  수직 해상도가 240, 480, 600, 720 및 1080인 MBR 스트림이 다음 RBOP 설정으로 플레이어에 전달된다고 가정해 보겠습니다.

  **RBOP 정책 설정:**

   * 720P - HDCP 필요
   * 480P - OP 없음

  다음 규칙이 각 변형에 적용됩니다.

  **스트림:**

   * 240, 480: 둘 다 480 미만입니다. OP가 필요하지 않으며 HDCP가 있거나 없는 스트림이 로드됩니다.
   * 600, 720: 둘 다 720 미만입니다. 재생에는 HDCP가 필요합니다.
   * 1080: > 720. 위의 규칙에서 찾을 수 없으므로 스트림이 차단 목록에 추가됨(오류 반환).

* **질문.** 일부 Android 장치에서 정의한 픽셀 수 제한이 정의된 대로 정확하게 적용되지 않습니다. 무슨 일이 일어나고 있는 거죠?

  **A.** 일부 Android 장치에서 프레임 크기가 일반 크기보다 약간 더 높게 보고됩니다. 이 상황을 해결하려면 프레임 크기( `maxPixel` 및 `pixelCount` 설정)을 20픽셀 위로 설정합니다. 예를 들어 다음 위치에서 위쪽으로 프레임 크기 설정을 조정합니다.

  ```
  { 
      "maxPixel": 800, 
      "pixelConstraints": [ 
          { "pixelCount": 532, 
            "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
            "analog": {"output": "REQUIRED"} 
          }, 
  ... 
  ```

  끝:

  ```
  { 
      "maxPixel": 820, 
      "pixelConstraints": [ 
          { "pixelCount": 552, 
            "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
            "analog": {"output": "REQUIRED"} 
          }, 
  ... 
  ```

  의 모든 인스턴스에 대해 `maxPixel` 및 `pixelCount`.
