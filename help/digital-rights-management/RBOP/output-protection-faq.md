---
description: 해상도 기반 출력 보호 사용에 대한 FAQ입니다.
seo-description: 해상도 기반 출력 보호 사용에 대한 FAQ입니다.
seo-title: RBOP FAQ
title: RBOP FAQ
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# RBOP FAQ {#rbop-faq}

해상도 기반 출력 보호 사용에 대한 FAQ입니다.

* **Q.** 픽셀 제한에 대한 디지털 출력 요구 사항을 정의할 *때 HDCP 버전을 종료하면 구문 분석/형식 오류가 발생하지만 HDCP 요구 사항은 없습니다. 이 경우 디지털 출력 요구 사항을 구성하려면 어떻게 해야 합니까?* A. **A.** 현재 클라이언트에서 HDCP 버전 검사가 지원되지 않으므로 HDCP 버전을 로 설정하는 것이 좋습니다 `1.0`. 이렇게 하면 HDCP 버전 검사가 지원될 때 구성이 올바르게 포맷되어 있고 나중에 일관됩니다. 다음 코드 조각은 이 HDCP 값이 있는 구성을 보여 줍니다.

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

* **Q.** RBOP *픽셀 제한은 서로 다르지만 범위를 기반으로 합니까?* A. **A.** RBOP 픽셀 제한은 다양한 기준을 기반으로 합니다. 각 픽셀 수는 지정된 수보다 작거나 같은 모든 픽셀 수에 대한 요구 사항을 정의하거나 둘 이상의 픽셀 제한이 있을 경우 해당 값보다 작은 최대 카운트를 정의합니다. 간단히 말해, 값은 각 세로 픽셀 수에 대한 최대 임계값으로 적용됩니다.

   세로 해상도가 240, 480, 600, 720 및 1080인 MBR 스트림이 다음 RBOP 설정으로 플레이어에 전달되었다고 가정합니다.

   **RBOP 정책 설정:**

   * 720P - HDCP 필요
   * 480P - OP 없음
   각 변형에 다음 규칙이 적용됩니다.

   **스트림:**

   * 240, 480:둘 다 &lt;= 480;OP는 필요하지 않으며 스트림은 HDCP가 있거나 없는 상태로 로드됩니다.
   * 600, 720:둘 다 &lt;= 720;재생에 HDCP가 필요합니다.
   * 1080년:> 720;스트림은 위의 규칙에 없으므로 블랙리스트에 포함됩니다(오류가 반환됨).


* **Q.** 일부 Android 장치에서 정의한 픽셀 수 제한이 정의된 대로 정확하게 적용되지 않습니다. 무슨 일이야?

   **A.** 일부 Android 장치는 프레임 크기를 일반 크기보다 약간 더 높게 보고합니다. 이 문제를 해결하려면 프레임 크기( `maxPixel` 및 `pixelCount` 설정)를 20픽셀만큼 위쪽으로 조정합니다. 예를 들어 다음 위치에서 프레임 크기 설정을 위쪽으로 조정합니다.

   ```
   { 
       "maxPixel":  
   
<b>800</b>,&quot;pixelConstraints&quot;:[{ &quot;pixelCount&quot;:\
<b>532</b>, &quot;디지털&quot;: [{&quot;output&quot;:&quot;REQUIRED&quot;, &quot;hdcp&quot;:{&quot;major&quot;:1, &quot;minor&quot;:0}}],&quot;아날로그&quot;:{&quot;output&quot;:&quot;REQUIRED&quot;}},...

```
to: 
```
{&quot;maxPixel&quot;:\
<b>820</b>,&quot;pixelConstraints&quot;:[{ &quot;pixelCount&quot;:\
<b>552</b>, &quot;디지털&quot;: [{&quot;output&quot;:&quot;REQUIRED&quot;, &quot;hdcp&quot;:{&quot;major&quot;:1, &quot;minor&quot;:0}}],&quot;아날로그&quot;:{&quot;output&quot;:&quot;REQUIRED&quot;}},...

```
throughout, for all instances of `maxPixel` and `pixelCount`.

