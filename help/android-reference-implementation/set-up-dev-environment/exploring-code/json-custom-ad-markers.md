---
title: 사용자 지정 광고 마커에 대한 JSON 개체
description: 사용자 지정 광고 마커에 대한 JSON 개체
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 사용자 지정 광고 마커에 대한 JSON 개체 {#json-object-for-custom-ad-markers}

유형이 사용자 지정 광고 마커인 경우 아래의 코드 블록은 &quot;세부 정보&quot; JSON 개체를 정의합니다.

IFeedItemAdapter:getStreamMetadata()에 의해 반환된 MetadataNode에는 2개의 항목이 포함되어 있습니다.
1. 유형의 키가 있는 항목 `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 및 이 반환한 MetadataNode 인스턴스의 값 `TimeRangeCollection.toMetadata()`.
1. 두 번째 항목에는 다음 유형의 키가 있습니다 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 을 값으로 *찾기 위치 조정* 아래 속성.

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
| 찾기 위치 조정 | MetadataNode에서 com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED 키의 값을 설정하는 데 사용되는 true 또는 false입니다. |
| 시간 범위 | 각 광고 마커의 시간 범위를 나타내는 JSON 개체의 배열입니다. 각 JSON 개체 항목은 com.adobe.mediacore.utils.TimeRange 인스턴스에 매핑됩니다. |
| time-ranges.begin | 광고 마커의 시작 시간을 나타내는 밀리초 단위 값입니다. |
| time-ranges.end | 광고 마커의 종료 시간을 나타내는 밀리초 단위 값입니다. |

사용자 지정 광고 마커의 작동 방식에 대한 자세한 내용은 TVSDK 설명서 를 참조하십시오.
