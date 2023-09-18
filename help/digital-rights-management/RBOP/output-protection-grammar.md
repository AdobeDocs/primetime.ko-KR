---
description: 이 섹션에서는 유효하고 잘못된 입력 옵션을 강조하고 생략된 옵션 필드를 해석하는 방법에 대해 설명하면서 구성 입력의 문법을 다룹니다.
title: RBOP 문법
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# RBOP 문법 {#rbop-grammar}

이 섹션에서는 유효하고 잘못된 입력 옵션을 강조하고 생략된 옵션 필드를 해석하는 방법에 대해 설명하면서 구성 입력의 문법을 다룹니다.

해상도 기반 출력 보호 문법은 규칙의 시퀀스로 정의되며, 각 규칙에는 유효한 여러 양식이 있을 수 있습니다.

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 문법 규칙 적용 {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>문법의 가독성을 향상시키기 위해 다음 속성이 문법에 반영되지 않지만 여전히 적용됩니다.

1. 개체 내에 정의된 쌍의 순서는 고정되지 않으므로 쌍의 순열은 모두 유효하다.

   예를 들어 다음과 같은 개체를 정의한 경우:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   그러면 다음 구조도 유효한 것으로 간주됩니다. =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 객체 내의 각 쌍에 대해 해당 쌍의 인스턴스는 지정된 객체의 지정된 인스턴스 내에 1개만 존재한다고 가정합니다.

   예를 들어 다음과 같은 개체를 정의한 경우:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   다음 인스턴스가 올바르지 않습니다. 두 개의 인스턴스가 있습니다. `foo` 동일한 개체 내의 쌍:

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   마찬가지로 다음과 같은 두 가지 객체가 있습니다.

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

   은 동일한 객체의 독립 인스턴스이므로 유효합니다.

1. 문자열 시퀀스 중 하나 이상을 선택할 수 있는 정의의 경우 문자열을 집합처럼 처리하십시오. 중복 항목은 단일 항목으로 처리됩니다. 예를 들어, `["foo", "bar", "foo", "baz"]` 은(는) 와 동일합니다. `["foo", "bar", "baz"]`

1. 숫자를 정의하기 위해 규칙 사이에 공백이 사용됩니다(예: `Digit Digits`), 단, 규칙을 적용할 때는 해당 공백을 사용해서는 안 됩니다.

   예를 들어, 숫자를 표현하면 *백이십삼* NonZeroInteger 규칙에 따라 다음과 같이 표현해야 합니다. `123` 보다 `1 2 3`, 규칙에 NonZeroDigit과 Digits 사이의 공백이 있더라도

1. 일부 규칙은 여러 양식을 허용합니다. 이 경우 다른 양식은 `'|'` 문자.

   예를 들어 이 규칙은 다음과 같습니다.

   ```
   Foo ::= "A" | "B" | "C"
   ```

   은(는) 의 인스턴스가 `Foo` 은 &quot;A&quot;, &quot;B&quot; 또는 &quot;C&quot;로 대체할 수 있습니다. 여러 줄에 걸쳐 있는 양식과 혼동하면 안 됩니다. 즉, 긴 양식을 더 읽기 쉽게 만드는 기능입니다.

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

## 의미 체계: 합법적이지만 잘못된 구성 {#section_709BE240FF0041D4A1B0A0A7544E4966}

다음 *샘플 출력 보호 구성* 주제는 의미론적 의미와 함께 타당한 구성을 제시하였다. 의 이전 섹션 *이* 주제에서는 구성에 대한 문법 규칙을 제공했습니다. 문법은 구문적 정확성을 보장하는 데 도움이 되지만, 구문적으로 정확하지 않은(즉, 논리적이지 않은) 구문적으로 합법적 구성이 있다. 이 섹션에는 다음과 같은 구성이 표시됩니다. *문법적으로* 합법적이지만 *의미상* 틀립니다. 이 섹션의 예는 논의 중인 시나리오를 설명하는 데 필요한 최소 구조로 줄었다는 점을 명심하십시오.

* 동일한 픽셀 카운트로 다수의 픽셀 제약을 정의하는 것은 부적합하다.

  ```
  {  
    "pixelConstraints":  
      [  
        { "pixelCount": 720 }  
      ]  
   }  
  ```

* 픽셀 수는 지정된 최대 픽셀 해상도를 초과할 수 없습니다.

  ```
  { 
    "maxPixel": 720, 
    "pixelConstraints": 
      [ 
        {"pixelCount": 1080} 
      ] 
  } 
  ```
