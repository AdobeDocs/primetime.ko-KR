---
seo-title: Primetime 광고를 위한 JSON 개체
title: Primetime 광고를 위한 JSON 개체
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: 아래 코드 블록은 유형 값이 Primetime 광고인 경우 JSON 개체에 대한 세부 사항을 정의합니다.
seo-description: 아래 코드 블록은 유형 값이 Primetime 광고인 경우 JSON 개체에 대한 세부 사항을 정의합니다.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Primetime 광고를 위한 JSON 개체 {#json-object-for-primetime-ads}

아래 코드 블록은 유형 값이 Primetime 광고인 경우 JSON 개체에 대한 세부 사항을 정의합니다.

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| 속성 | 설명 |
|---|---|
| domain | Primetime 광고 도메인을 사용하여 광고 요청 |
| mediaid | Primetime 광고에 설정된 미디어입니다. |
| zoneid | Primetime 광고 zoneid 자세한 내용은 Primetime 광고 설명서를 참조하십시오. |
| 타깃팅 | 컨텐츠의 특정 광고를 타깃팅하는 데 사용되는 키/값 쌍의 배열입니다. |

이러한 속성의 값에 대한 자세한 내용은 [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) .AuditudeSettings를 참조하십시오.