---
description: 광고 삽입을 통해 실시간 스트리밍을 위한 VOD(Video-On-Demand) 광고, 광고 추적 및 광고 재생을 통한 선형 스트리밍을 해결할 수 있습니다. TVSDK는 광고 서버에 필요한 요청을 수행하고, 지정된 컨텐츠에 대한 광고에 대한 정보를 수신하며, 광고를 단계적으로 전달합니다.
seo-description: 광고 삽입을 통해 실시간 스트리밍을 위한 VOD(Video-On-Demand) 광고, 광고 추적 및 광고 재생을 통한 선형 스트리밍을 해결할 수 있습니다. TVSDK는 광고 서버에 필요한 요청을 수행하고, 지정된 컨텐츠에 대한 광고에 대한 정보를 수신하며, 광고를 단계적으로 전달합니다.
seo-title: 광고 삽입
title: 광고 삽입
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# 개요 {#inserting-ads-overview}

광고 삽입을 통해 실시간 스트리밍을 위한 VOD(Video-On-Demand) 광고, 광고 추적 및 광고 재생을 통한 선형 스트리밍을 해결할 수 있습니다. TVSDK는 광고 서버에 필요한 요청을 수행하고, 지정된 컨텐츠에 대한 광고에 대한 정보를 수신하며, 광고를 단계적으로 전달합니다.

*`ad break`*&#x200B;에는 차례로 재생되는 하나 이상의 광고가 포함되어 있습니다. TVSDK는 하나 이상의 광고 중단의 구성원으로 기본 컨텐츠에 광고를 삽입합니다.

## 프리롤 광고 비활성화 {#disable-preroll-ads}

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
