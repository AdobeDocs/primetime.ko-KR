---
title: Just-in-Time 코드 변환
description: Just-in-Time 코드 변환
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Just-in-Time 코드 변환 {#just-in-time-transcoding}

Primetime Ad Insertion은 호환되지 않는 광고 크리에이티브를 컨텐츠 스트림에서 제대로 재생할 수 있도록 적시 코드 변환 및 패키징을 제공합니다. 또한 클라이언트측 광고 추적에 사용할 수 있는 광고 조각에 ID3 패킷을 삽입할 수도 있습니다.
일반적인 워크플로우는 다음과 같습니다.

1. Adobe Primetime Ad Insertion은 고객의 광고 서버에서 광고/크리에이티브를 가져옵니다.

1. 광고의 크리에이티브 포맷이 기본적으로 콘텐츠 스트림과 호환되는 경우 크리에이티브가 매니페스트에 삽입됩니다.

1. 광고의 크리에이티브 형식이 기본적으로 호환되지 않는 경우(예: .mp4, .mov, .webm), Primetime Ad Insertion은 지정된 CDN에서 사전 코드 처리된 광고 버전을 검색합니다. 하나가 발견되면 해당 광고가 삽입됩니다. 그렇지 않으면 해당 광고가 코드 변환 큐에 대기됩니다.

1. 광고 크리에이티브가 코드 변환된 후 Primetime Ad Insertion은 해당 광고 자산에 대한 모든 후속 요청을 매니페스트에 결합합니다.

Primetime Ad Insertion은 대부분의 비디오 및 선형 형식에 대해 코드 변환 기능을 지원합니다. 광고 크리에이티브 코드 변환은 일반적으로 3분 이내에 발생합니다. 자세한 내용은 Primetime 지원 담당자에게 문의하십시오.
