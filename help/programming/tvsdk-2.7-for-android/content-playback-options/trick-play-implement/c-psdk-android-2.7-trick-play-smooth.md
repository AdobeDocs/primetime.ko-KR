---
description: 시스템에서 하드웨어 지원 디코딩에 액세스할 수 있는 경우 iFrame 형식을 사용하여 순수 소프트웨어 TVSDK 구현보다 더 원활한 트릭 플레이를 수행할 수 있습니다.
title: 매끄러운 트릭 플레이 작업
exl-id: 2dcc8ee2-78a1-4ec8-b876-e06e5ec1e398
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 매끄러운 트릭 플레이 작업 {#smoother-trick-play-operations}

시스템에서 하드웨어 지원 디코딩에 액세스할 수 있는 경우 iFrame 형식을 사용하여 순수 소프트웨어 TVSDK 구현보다 더 원활한 트릭 플레이를 수행할 수 있습니다.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

iFrame 형식을 사용하면 트릭 재생 작업이 매끄럽지 않게 됩니다. 더 매끄러운 트릭 재생 작업에서는 일반(iFrame 아님) 프로필, 하드웨어 디코딩 지원 및 증가된 프레임 속도를 사용합니다. 상이한 하드웨어-보조 디코딩 디바이스들은 상이한 능력들을 갖는다. 이중 속도는 초당 60프레임(FPS)이 필요하며 4중 속도는 120FPS가 필요합니다.

>[!IMPORTANT]
>
>Adobe은 최신 Android 장치의 경우 재생을 두 배 속도로 제한하고 이전 Android 장치의 경우 기능을 사용하지 말 것을 권장합니다.

더 원활한 트릭 플레이를 달성하려면, 세트 `ABRControlParameters.maxPlayoutRate` 원하는 일반 속도의 배수로 변경합니다(예: 2배 속도의 경우 2.0). 다음에 대한 후속 호출인 경우 `MediaPlayer.setRate()` 에는 사용자가 설정한 값보다 작거나 같은 인수가 있습니다. `maxPlayoutRate`, TVSDK는 일반 프로필을 사용하여 더 원활한 트릭 플레이를 수행합니다. 그렇지 않으면 trickplay 작업에 iFrame 프로필을 사용합니다.
