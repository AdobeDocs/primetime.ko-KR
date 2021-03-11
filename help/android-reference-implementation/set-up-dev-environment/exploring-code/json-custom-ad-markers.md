---
title: 사용자 정의 광고 마커용 JSON 개체
description: 사용자 정의 광고 마커용 JSON 개체
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 사용자 지정 광고 마커 {#json-object-for-custom-ad-markers}용 JSON 개체

아래 코드 블록은 유형이 사용자 지정 광고 표시자일 때 &quot;세부 사항&quot; JSON 개체를 정의합니다.

IFeedItemAdapter:getStreamMetadata()에 의해 반환된 MetadataNode에는 다음 2개의 항목이 포함됩니다.
1. `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 유형의 키와 `TimeRangeCollection.toMetadata()`에서 반환되는 MetadataNode 인스턴스의 값을 갖는 항목.
1. 두 번째 항목에는 *adjust-seek-position* 특성 값이 있는 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 유형의 키가 있습니다.

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| 속성 | 설명 |
|---|---|
| seek-position 조정 | true 또는 false - MetadataNode에서 key com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED의 값을 설정하는 데 사용됩니다. |
| 시간 범위 | 각 광고 마커의 시간 범위를 나타내는 JSON 개체 배열입니다. 각 JSON 개체 항목은 com.adobe.mediacore.utils.TimeRange 인스턴스에 매핑됩니다. |
| time-ranges.begin | 광고 마커의 시작 시간을 나타내는 ms의 값입니다. |
| time-ranges.end | 광고 마커의 종료 시간을 나타내는 ms의 값입니다. |

사용자 정의 광고 마커가 작동하는 방법에 대한 자세한 내용은 TVSDK 설명서를 참조하십시오.
