---
title: Primetime 광고에 대한 JSON 개체
description: 아래 코드 블록은 유형 값이 Primetime 광고인 경우 세부 JSON 개체를 정의합니다.
exl-id: b1392781-2dfb-4934-b1ce-1c761cbfb22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Primetime 광고에 대한 JSON 개체 {#json-object-for-primetime-ads}

아래 코드 블록은 유형 값이 Primetime 광고인 경우 세부 JSON 개체를 정의합니다.

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
| 도메인 | 광고 요청에 사용할 Primetime 광고 도메인입니다. |
| mediaid | 이 컨텐츠에 대해 Primetime 광고에 설정된 mediaid. |
| zoneid | Primetime 광고 zoneid. 자세한 내용은 Primetime 광고 설명서 를 참조하십시오. |
| 타겟팅 | 콘텐츠의 특정 광고를 타겟팅하는 데 사용되는 키/값 쌍의 배열입니다. |

다음을 참조하십시오 [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 를 참조하십시오.
