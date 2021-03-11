---
description: 시스템에 하드웨어 지원 디코딩에 대한 액세스 권한이 있는 경우 iFrame 형식을 사용하여 순수한 소프트웨어 TVSDK 구현보다 더 매끄러운 트릭 재생을 수행할 수 있습니다.
title: 매끄러운 트릭 재생 작업
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# 매끄러운 트릭 재생 작업 {#smoother-trick-play-operations}

시스템에 하드웨어 지원 디코딩에 대한 액세스 권한이 있는 경우 iFrame 형식을 사용하여 순수한 소프트웨어 TVSDK 구현보다 더 매끄러운 트릭 재생을 수행할 수 있습니다.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

iFrame 형식을 사용하면 매끄러운 트릭 재생 작업이 수행됩니다. 매끄러운 트릭 재생 작업은 일반적인(iFrame 아님) 프로필, 하드웨어 디코딩 지원 및 증가된 프레임 속도를 사용합니다. 하드웨어 지원 디코딩 장치마다 기능이 다릅니다. 2배 속도에는 60FPS(초당 프레임 수), 4배 속도에는 120FPS가 필요합니다.

>[!IMPORTANT]
>
>Adobe에서는 신규 Android 장치의 재생을 두 배로 제한하고 이전 Android 장치용 기능을 사용하지 않는 것이 좋습니다.

매끄러운 트릭 재생을 수행하려면 `ABRControlParameters.maxPlayoutRate`을 원하는 여러 일반 속도(예: 두 배 속도의 경우 2.0)로 설정합니다. `MediaPlayer.setRate()`에 대한 후속 호출에 `maxPlayoutRate`에 대해 설정한 값보다 작거나 같은 인수가 있는 경우 TVSDK는 일반적인 프로파일을 사용하여 보다 매끄러운 트릭 재생을 실행합니다. 그렇지 않으면 trickplay 작업에 iFrame 프로필을 사용합니다.