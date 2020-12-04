---
seo-title: 사용자 정의 광고 마커용 JSON 개체
title: 사용자 정의 광고 마커용 JSON 개체
uuid: 2c05d9ce-a22f-4829-bfea-9dcf0dc7cd6d
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 사용자 지정 광고 마커 {#json-object-for-custom-ad-markers}에 대한 JSON 개체

아래 코드 블록은 유형이 사용자 지정 광고 마커일 때 &quot;세부 사항&quot; JSON 개체를 정의합니다.

IFeedItemAdapter:getStreamMetadata()가 반환하는 MetadataNode에는 다음 2개의 항목이 포함됩니다.
1. `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` 형식의 키와 `TimeRangeCollection.toMetadata()`이(가) 반환하는 MetadataNode 인스턴스의 값을 갖는 항목입니다.
1. 두 번째 항목에는 *adjust-seek-position* 특성의 값이 있는 `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 유형의 키가 있습니다.

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
| 조정-검색 위치 | true 또는 false 키, com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED의 값을 설정하는 데 사용됩니다. |
| 시간 범위 | 각 광고 마커의 시간 범위를 나타내는 JSON 개체 배열. 각 JSON 개체 항목은 com.adobe.mediacore.utils.TimeRange 인스턴스에 매핑됩니다. |
| time-ranges.begin | 광고 마커의 시작 시간을 나타내는 ms의 값입니다. |
| time-ranges.end | 광고 마커의 종료 시간을 나타내는 ms의 값입니다. |

사용자 지정 광고 마커의 작동 방식에 대한 자세한 내용은 TVSDK 설명서를 참조하십시오.
