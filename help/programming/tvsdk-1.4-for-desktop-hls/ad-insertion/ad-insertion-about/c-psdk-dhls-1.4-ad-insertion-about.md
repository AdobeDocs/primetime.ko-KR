---
description: 광고 삽입은 주문형 비디오(VOD), 라이브 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 하고, 지정된 컨텐츠에 대한 광고 정보를 수신하고, 단계별로 광고를 컨텐츠에 배치합니다.
title: 광고 삽입
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 개요 {#inserting-ads-overview}

광고 삽입은 주문형 비디오(VOD), 라이브 스트리밍, 광고 추적 및 광고 재생을 통한 선형 스트리밍 광고를 해결합니다. TVSDK는 광고 서버에 필요한 요청을 하고, 지정된 컨텐츠에 대한 광고 정보를 수신하고, 단계별로 광고를 컨텐츠에 배치합니다.

An *`ad break`* 에는 차례로 재생되는 하나 이상의 광고가 포함되어 있습니다. TVSDK는 하나 이상의 광고 브레이크의 구성원으로 기본 콘텐츠에 광고를 삽입합니다.

## 프리롤 광고 비활성화 {#disable-preroll-ads}

프리롤을 비활성화하려면 기본 영업 기회 생성자를 프리롤 호출하지 않도록 변경하십시오. 기본 영업 기회 생성기는 다음과 같습니다.

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

라이브 스트림에서 프리롤을 비활성화하려면 SpliceOutOpportunityGenerator만 포함하도록 위의 내용을 변경합니다.

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
