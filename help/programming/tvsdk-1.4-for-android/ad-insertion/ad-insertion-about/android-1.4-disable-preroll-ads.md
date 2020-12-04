---
description: 'null'
seo-description: 'null'
seo-title: 프리롤 광고 비활성화
title: 프리롤 광고 비활성화
uuid: 2e307a58-49f2-43d6-908b-97684ad6e3d3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '45'
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

라이브 스트림에서 프리롤 기능을 비활성화하려면 위의 내용을 SpliceOutOpportunityGenerator만 포함하도록 변경하십시오.

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

