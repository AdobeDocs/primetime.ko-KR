---
title: 프리롤 광고 비활성화
description: 프리롤 광고 비활성화
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---


# 프리롤 광고 비활성화{#disable-pre-roll-ads}

프리롤 기능을 비활성화하려면 기본 기회 생성기를 변경하여 프리롤 호출을 하지 않도록 하십시오. 기본 기회 생성기는 다음과 같습니다.

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

실시간 스트림에서 프리롤 기능을 비활성화하려면 SpliceOutOpportunityGenerator만 포함하도록 위의 내용을 변경합니다.

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

