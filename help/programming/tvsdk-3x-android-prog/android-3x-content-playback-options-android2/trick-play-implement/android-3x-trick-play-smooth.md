---
description: 시스템에서 하드웨어 지원 디코딩을 이용할 수 있는 경우 iFrame 포맷을 사용하여 순수한 소프트웨어 TVSDK 구현보다 매끄러운 트릭 재생을 구현할 수 있습니다.
seo-description: 시스템에서 하드웨어 지원 디코딩을 이용할 수 있는 경우 iFrame 포맷을 사용하여 순수한 소프트웨어 TVSDK 구현보다 매끄러운 트릭 재생을 구현할 수 있습니다.
seo-title: 매끄러운 트릭 재생 작업
title: 매끄러운 트릭 재생 작업
uuid: 959d6c67-b64f-4666-8de7-54d247459fd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 매끄러운 트릭 재생 작업 {#smoother-trick-play-operations}

시스템에서 하드웨어 지원 디코딩을 이용할 수 있는 경우 iFrame 포맷을 사용하여 순수한 소프트웨어 TVSDK 구현보다 매끄러운 트릭 재생을 구현할 수 있습니다.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

iFrame 포맷을 사용하면 매끄럽지 않은 트릭 재생 작업이 이루어집니다. 매끄러운 트릭 재생 작업은 일반적인(iFrame 아님) 프로필, 하드웨어 디코딩 지원 및 향상된 프레임 속도를 사용합니다. 하드웨어 지원 디코딩 장치마다 기능이 다릅니다. 이중 속도는 초당 60프레임(FPS), 4중 속도는 120FPS가 필요합니다.

>[!IMPORTANT]
>
>최신 Android 장치에서는 재생을 두 배로 제한하고 이전 Android 장치에서는 이 기능을 사용하지 않는 것이 좋습니다.

더 매끄러운 트릭 재생을 수행하려면 원하는 여러 일반 속도(예: 2.0, 두 배 속도) `ABRControlParameters.maxPlayoutRate` 로 설정합니다. 후속 호출에 대해 설정한 값보다 작거나 같은 인수가 `MediaPlayer.setRate()` 있는 `maxPlayoutRate`경우 TVSDK는 일반적인 프로파일을 사용하여 보다 매끄러운 트릭 재생을 수행합니다. 그렇지 않으면 iFrame 프로파일을 사용하여 트릭플레이 작업을 수행할 수 있습니다.