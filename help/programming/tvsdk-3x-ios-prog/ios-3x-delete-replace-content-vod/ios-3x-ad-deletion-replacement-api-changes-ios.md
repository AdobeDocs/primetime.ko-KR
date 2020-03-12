---
description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 교체하는 것을 지원합니다.
seo-description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 교체하는 것을 지원합니다.
seo-title: 광고 삭제 및 교체 API 변경 사항
title: 광고 삭제 및 교체 API 변경 사항
uuid: 3689d31f-4feb-4ea5-ac49-ef2e71472f4b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 광고 삭제 및 교체 API 변경 사항 {#ad-deletion-and-replacement-api-changes}

TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제 및 교체하는 것을 지원합니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 컨텐츠의 섹션을 광고 관련 컨텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

TVSDK에서 다음 변경 사항은 광고 삭제 및 바꾸기를 지원합니다.

**새로운 API**

* `PTTimeRangeCollection` 은 사전 정의된 범위 및 유형을 정의하는 공개 클래스입니다.

   * `property PTTimeRangeCollectionType type` 시간 범위 유형을 나타냅니다.
   * `property NSArray* ranges` 을 사용하여 시간 범위를 설정합니다.

      배열에서 예상되는 객체 유형은 `PTReplacementTimeRange` 또는 `CMTimeRange`입니다.

      >[!TIP]
      >
      >배열의 모든 개체는 동일한 유형이어야 합니다.

   * `PTTimeRangeCollectionType` 는 `PTTimeRangeCollection`다음에 정의된 범위의 동작을 정의하는 열거형입니다.

      * `PTTimeRangeCollectionTypeMarkRanges`:범위의 유형은 *표시입니다*. 범위는 컨텐츠의 범위를 광고로 표시하는 데 사용됩니다.

      * `PTTimeRangeCollectionTypeDeleteRanges`:범위의 유형은 삭제입니다. 광고 삽입 전에 기본 컨텐츠에서 정의된 범위가 제거됩니다.
      * `PTTimeRangeCollectionTypeReplaceRanges`:범위 유형은 바꾸기입니다. 정의된 범위가 기본에서 광고로 대체됩니다(광고 신호 모드가 로 `PTAdSignalingModeCustomTimeRanges`설정됨).

* `PTReplacementTimeRange` - 다음과 같은 단일 범위를 정의하는 새 공개 클래스 `PTTimeRangeCollection`:

   * `property CMTimeRange range` - 범위의 시작 및 지속 시간을 정의합니다.
   * `property long replacementDuration` - 유형이 `TimeRangeCollection` 인 `PTTimeRangeCollectionTypeReplaceRanges`경우 `replacementDuration` 는 지속 `replacementDuration`기간을 사용하여 배치 기회(광고 삽입)를 생성하는 데 사용됩니다. 이 `replacementDuration` 옵션이 설정되지 않은 경우 광고 서버는 해당 배치 기회의 기간 및 광고 수를 결정합니다.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - 새로운 유형의 `PTAdSignalingMode`을 추가했습니다. 이 모드는 대체 범위를 기준으로 광고 삽입 `PTTimeRangeCollection` 유형과 함께 `PTTimeRangeCollectionReplace` 사용됩니다.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - 재생 내용의 표시/삭제/바꾸기 범위에 사용된 시간 범위를 설정하는 경우

* 경고 로그:

   * `UNDEFINED_TIME_RANGES`

      * 유형 - 경고
      * 설명 - 광고 신호 모드는 사용자 지정 범위로 정의되지만 사용자 지정 범위는 정의되지 않습니다.
   * `INVALID_TIME_RANGES`

      * 유형 - 경고
      * 설명 - 하나 이상의 시간 범위가 잘못되어 무시되거나 수정됩니다.


**더 이상 사용되지 않는 API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - 이전에 이 속성은 마크업에 대한 C3 범위를 정의하는 데 사용되었습니다. 이제 이러한 범위는 를 통해 설정되므로 더 이상 사용되지 않습니다 `PTTimeRangeCollection`.