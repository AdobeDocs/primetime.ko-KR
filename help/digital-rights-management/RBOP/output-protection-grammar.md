---
description: 이 섹션에서는 구성 입력의 문법, 유효하고 잘못된 입력 옵션을 강조하고, 생략된 선택적 필드를 해석하는 방법을 설명합니다.
seo-description: 이 섹션에서는 구성 입력의 문법, 유효하고 잘못된 입력 옵션을 강조하고, 생략된 선택적 필드를 해석하는 방법을 설명합니다.
seo-title: RBOP 문법
title: RBOP 문법
uuid: d9064e39-593a-4767-b835-287640b4c94a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---


# RBOP 문법 {#rbop-grammar}

이 섹션에서는 구성 입력의 문법, 유효하고 잘못된 입력 옵션을 강조하고, 생략된 선택적 필드를 해석하는 방법을 설명합니다.

해상도 기반 출력 보호 문법은 규칙 시퀀스로 정의되며, 여기서 각 규칙에는 유효한 여러 양식이 있을 수 있습니다.

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 문법 규칙 적용 {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>문법의 가독성을 높이기 위해 다음 속성은 문법 내에 반영되지 않지만 여전히 true입니다.

1. 개체 내에 정의된 쌍의 순서는 고정되지 않습니다.따라서 이 쌍의 변형이 유효합니다.

   예를 들어 다음과 같은 객체를 정의한 경우:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   다음 구조도 유효하다고 간주됩니다.=

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 객체 내의 각 쌍에 대해 주어진 객체의 지정된 인스턴스 내에 해당 쌍의 인스턴스가 1개만 있다고 가정합니다.

   예를 들어 다음과 같은 객체를 정의한 경우:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   동일한 개체 내에 두 개의 `foo` 쌍이 있으므로 다음 인스턴스가 유효하지 않습니다.

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   마찬가지로 다음과 같은 두 개의 개체가 있습니다.

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   및:

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   는 동일한 개체의 독립 인스턴스이므로 유효합니다.

1. 문자열 순서를 하나 이상 선택할 수 있는 정의에 대해서는 문자열을 집합과 같이 취급하여 중복 항목을 단일 항목으로 처리합니다. 예를 들어 `["foo", "bar", "foo", "baz"]`은 `["foo", "bar", "baz"]`와 같습니다.

1. 숫자를 정의할 때 규칙 사이에 공백이 사용되지만(예: `Digit Digits`) 규칙을 적용할 때는 이 공백이 사용되지 않습니다.

   예를 들어 NonZeroInteger 규칙당 숫자 *123개*&#x200B;를 표현하는 경우 규칙에 NonZeroDigit와 숫자 사이의 공백이 포함되어 있더라도 `1 2 3`이 아닌 `123`로 표현되어야 합니다.

1. 일부 규칙에서는 여러 양식을 사용할 수 있습니다. 이러한 경우 다른 양식은 `'|'` 문자로 구분됩니다.

   예를 들어 이 규칙은 다음과 같습니다.

   ```
   Foo ::= "A" | "B" | "C"
   ```

   즉, `Foo`의 인스턴스가 &quot;A&quot;, &quot;B&quot; 또는 &quot;C&quot;로 대체될 수 있습니다. 이는 여러 줄에 걸쳐 있는 양식과 혼동하지 마십시오.이는 더 긴 양식을 보다 읽기 쉽게 만드는 기능입니다.

## 문법 {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## 의미 체계:유효하지만 잘못된 구성 {#section_709BE240FF0041D4A1B0A0A7544E4966}

*샘플 출력 보호 구성* 항목에서는 의미 의미와 함께 유효한 구성을 보여 줍니다. *이* 항목의 이전 섹션에 구성에 대한 문법 규칙이 표시되었습니다. 문법은 문법의 정확성을 보장하는 데 도움을 주지만, 문법에 맞지 않는 합법적인 구성이 있다(즉, 논리적이지 않다). 이 섹션은 *구문상* 합법이지만 *중간 수준*&#x200B;이 잘못된 구성을 나타냅니다. 이 섹션의 예는 토론 중인 시나리오를 설명하는 데 필요한 최소 구조로 줄었습니다.

* 픽셀 수가 동일한 여러 픽셀 제한을 정의하는 것은 잘못되었습니다.

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* 픽셀 수는 지정한 최대 픽셀 해상도를 초과할 수 없습니다.

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
