---
description: TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제하고 바꿀 수 있습니다.
title: 광고 삭제 및 대체 API 변경 사항
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 광고 삭제 및 대체 API 변경 사항 {#ad-deletion-and-replacement-api-changes}

TVSDK는 VOD 스트림에서 광고 콘텐츠를 프로그래밍 방식으로 삭제하고 바꿀 수 있습니다.

삭제 및 바꾸기 기능은 사용자 지정 광고 마커 기능을 확장합니다. 사용자 지정 광고 마커는 기본 콘텐츠의 섹션을 광고 관련 콘텐츠 기간으로 표시합니다. 이러한 시간 범위를 표시하는 것 외에도 시간 범위를 삭제하고 바꿀 수도 있습니다.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

TVSDK의 다음 변경 사항은 광고 삭제 및 교체를 지원합니다.

**새 API**

* `PTTimeRangeCollection` 는 사전 정의된 범위 집합 및 유형을 정의하는 공용 클래스입니다.

   * `property PTTimeRangeCollectionType type` 시간 범위의 유형을 나타냅니다.
   * `property NSArray* ranges` 은 시간 범위를 설정하는 데 사용됩니다.

     배열에서 예상되는 개체 유형은 다음과 같습니다. `PTReplacementTimeRange` 또는 `CMTimeRange`.

     >[!TIP]
     >
     >배열의 모든 개체는 같은 유형이어야 합니다.

   * `PTTimeRangeCollectionType` 는에 정의된 범위의 동작을 정의하는 열거형입니다. `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: 범위의 유형은 다음과 같습니다. *표시*. 범위는 콘텐츠의 범위를 광고로 표시하는 데 사용됩니다.

      * `PTTimeRangeCollectionTypeDeleteRanges`: 범위 유형은 삭제입니다. 정의된 범위는 광고를 삽입하기 전에 기본 콘텐츠에서 제거됩니다.
      * `PTTimeRangeCollectionTypeReplaceRanges`: 범위 유형은 대체입니다. 정의된 범위가 기본 항목에서 Ads로 대체됩니다(광고 시그널링 모드가 다음으로 설정됨). `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - 의 단일 범위를 정의하는 새 공용 클래스 `PTTimeRangeCollection`:

   * `property CMTimeRange range` - 범위의 시작 및 기간을 정의합니다.
   * `property long replacementDuration` - 유형이 다음과 같은 경우 `TimeRangeCollection` 은(는) `PTTimeRangeCollectionTypeReplaceRanges`, `replacementDuration` 은 기간이 인 배치 기회(광고 삽입)를 만드는 데 사용됩니다. `replacementDuration`. 다음과 같은 경우 `replacementDuration` 가 설정되지 않은 경우 광고 서버는 해당 배치 기회에 대한 광고 기간 및 수를 결정합니다.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - 새 유형의 을(를) 추가함 `PTAdSignalingMode`. 이 모드는 `PTTimeRangeCollection` 유형 `PTTimeRangeCollectionReplace` 대체 범위를 기반으로 한 광고 삽입용.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - 재생 콘텐츠의 범위 표시/삭제/바꾸기에 사용되는 시간 범위를 설정합니다.

* 경고 로그:

   * `UNDEFINED_TIME_RANGES`

      * 유형 - 경고
      * 설명 - 광고 신호 모드는 사용자 지정 범위로 정의되지만 사용자 지정 범위는 정의되지 않습니다.

   * `INVALID_TIME_RANGES`

      * 유형 - 경고
      * 설명 - 하나 이상의 시간 범위가 잘못되어 무시되거나 수정됩니다.

**더 이상 사용되지 않는 API**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - 이 속성은 이전에 표시를 위한 C3 범위를 정의하는 데 사용되었습니다. 이러한 범위는 를 통해 설정되므로 이제 더 이상 사용되지 않습니다. `PTTimeRangeCollection`.
