---
description: TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에 대한 광고 크리에이티브 선택의 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브에 대한 소스 URL 변환 규칙을 정의할 수도 있습니다.
keywords: 크리에이티브 선택 규칙;AdobeTVSDKConfig;광고 크리에이티브 우선 순위;변환 규칙
title: 광고 크리에이티브 선택 규칙 업데이트
exl-id: b4249936-d658-49fb-85af-ebd8e1211d55
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 개요 {#update-ad-creative-selection-rules-overview}

TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에 대한 광고 크리에이티브 선택의 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브에 대한 소스 URL 변환 규칙을 정의할 수도 있습니다.

비디오 플레이어가 광고 서버에 요청할 때 VAST/VMAP 응답에는 일반적으로 여러 광고 크리에이티브( `MediaFile` elements): 각각 다른 컨테이너-코덱 버전에 URL을 제공합니다. 경우에 따라 VAST/VMAP 응답의 광고 크리에이티브가 각각 광고에 대한 다른 비트율을 제공합니다. 이러한 광고 크리에이티브에 대한 자체 우선 순위 및 변형 규칙을 지정하려면 다음에서 수행할 수 있습니다. [!DNL AdobeTVSDKConfig.json] 구성 파일입니다.

>[!IMPORTANT]
>
>* TVSDK 구성 파일의 이름을 변경하지 마십시오. 이름은 유지해야 합니다. [!DNL AdobeTVSDKConfig.json].
>* 이 파일은 번들에 액세스할 수 있는 모든 위치에 배치할 수 있습니다.
>


에서 두 가지 유형의 규칙을 지정할 수 있습니다. [!DNL AdobeTVSDKConfig.json]: *우선 순위* 규칙 및 *정규화* 규칙.

**[!UICONTROL Disabling Pre-Roll]**

프리롤을 비활성화하려면 프리롤 호출을 수행하지 않도록 기본 영업 기회 생성기를 변경해야 합니다. 기본적으로 TVSDK는 다음 기회 생성기를 사용합니다.

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

라이브 스트림에서 프리롤을 비활성화하려면 SpliceOutOpportunityGenerator만 포함하도록 변경해야 합니다.

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```
