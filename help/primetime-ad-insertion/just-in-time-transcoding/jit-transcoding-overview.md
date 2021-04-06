---
title: 적시 트랜스코딩
description: 적시 트랜스코딩
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 적시 트랜스코딩 {#just-in-time-transcoding}

Primetime Ad Insertion은 호환되지 않는 광고 크리에이티브를 컨텐츠 스트림에서 제대로 재생할 수 있도록 적시 트랜스코딩 및 패키징 기능을 제공합니다. 또한 클라이언트측 광고 추적에 사용할 수 있는 광고 조각에 ID3 패킷을 삽입할 수도 있습니다.
일반적인 워크플로우는 다음과 같습니다.

1. Adobe Primetime Ad Insertion은 고객의 광고 서버에서 광고/크리에이티브를 가져옵니다.

1. 광고 크리에이티브 형식이 컨텐츠 스트림과 기본적으로 호환되면 크리에이티브가 매니페스트에 삽입됩니다.

1. 광고의 크리에이티브 형식이 기본적으로 호환하지 않는 경우(예: .mp4, .mov, .webm), Primetime Ad Insertion은 지정된 CDN에서 광고의 사전 코딩된 버전을 검색합니다. 광고가 발견되면 광고가 삽입됩니다.그렇지 않으면 광고가 코드 변환에 대해 큐에 오르게 됩니다.

1. 광고 크리에이티브가 트랜스코딩되면 Primetime Ad Insertion은 해당 광고 에셋에 대한 모든 후속 요청을 매니페스트에 연결합니다.

Primetime Ad Insertion은 대부분의 비디오 및 선형 포맷에 대한 트랜스코딩을 지원합니다. 광고 크리에이티브 트랜스코딩은 일반적으로 3분 이내에 발생합니다. 자세한 내용은 Primetime 지원 담당자에게 문의하십시오.
