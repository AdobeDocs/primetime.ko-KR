---
description: TVSDK는 VOD 스트림에서 광고 컨텐츠의 프로그래머틱 삭제 및 대체를 지원합니다.
title: 광고 삭제 및 교체 API 변경 사항
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 광고 삭제 및 교체 API 변경 사항 {#ad-deletion-and-replacement-api-changes}

TVSDK는 VOD 스트림에서 광고 컨텐츠의 프로그래머틱 삭제 및 대체를 지원합니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 컨텐츠의 섹션을 광고 관련 컨텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

TVSDK 지원 및 삭제 및 대체에서 다음 변경 사항이 적용됩니다.

**새 API**

* `PTTimeRangeCollection` 는 미리 정의된 범위 세트와 유형을 정의하는 공개 클래스입니다.

   * `property PTTimeRangeCollectionType type` 시간 범위 유형을 나타냅니다.
   * `property NSArray* ranges` 시간 범위를 설정하는 데 사용됩니다.

      배열에 있는 개체 유형은 `PTReplacementTimeRange` 또는 `CMTimeRange`입니다.

      >[!TIP]
      >
      >배열의 모든 개체는 같은 유형이어야 합니다.

   * `PTTimeRangeCollectionType` 는 다음 항목에 정의된 범위의 비헤이비어를 정의하는 열거형입니다.  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`:범위의 유형은  *표시입니다*. 범위는 컨텐츠의 범위를 광고로 표시하는 데 사용됩니다.

      * `PTTimeRangeCollectionTypeDeleteRanges`:범위 유형은 삭제입니다. 광고 삽입 전에 기본 컨텐츠에서 정의된 범위가 제거됩니다.
      * `PTTimeRangeCollectionTypeReplaceRanges`:범위 유형은 바꾸기입니다. 정의된 범위가 기본에서 광고로 바뀝니다(광고 신호 모드는 `PTAdSignalingModeCustomTimeRanges`으로 설정됨).

* `PTReplacementTimeRange` - 다음 범위의 단일 범위를 정의하는 새 공개  `PTTimeRangeCollection`클래스:

   * `property CMTimeRange range` - 범위의 시작 및 지속 시간을 정의합니다.
   * `property long replacementDuration` - 유형 `TimeRangeCollection` 이  `PTTimeRangeCollectionTypeReplaceRanges`이면 `replacementDuration` 는 지속 시간이 있는 배치 기회(광고 삽입)를 만드는 데  `replacementDuration`사용됩니다. `replacementDuration`이(가) 설정되어 있지 않으면 광고 서버가 해당 배치 기회의 지속 시간과 광고 수를 결정합니다.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - 새로운 유형의 항목이 추가되었습니다 `PTAdSignalingMode`. 이 모드는 `PTTimeRangeCollection`과(와) 함께 사용하여 대체 범위를 기반으로 광고를 삽입합니다.`PTTimeRangeCollectionReplace`

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - 재생 내용의 표시/삭제/바꾸기 범위에 사용된 시간 범위를 설정하는 경우

* 경고 로그:

   * `UNDEFINED_TIME_RANGES`

      * 유형 - 경고
      * 설명 - 광고 신호 모드는 사용자 지정 범위로 정의되지만 사용자 지정 범위는 정의되지 않습니다.
   * `INVALID_TIME_RANGES`

      * 유형 - 경고
      * 설명 - 하나 이상의 시간 범위가 유효하지 않으며 무시되거나 수정됩니다.


**사용되지 않는 API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - 이 속성은 이전에 표시를 위한 C3 범위를 정의하는 데 사용되었습니다. 이제 이 범위는 `PTTimeRangeCollection`을 통해 설정되므로 더 이상 사용되지 않습니다.