---
title: 시간 기반 규칙 개요
description: 시간 기반 규칙 개요
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 시간 기반 규칙 {#time-based-rules}

Primetime DRM은 시간 기반 라이센스 제한의 &quot;소프트 시행&quot;을 사용합니다. 비디오 재생 중에 시간 권한이 만료되는 경우 Primetime DRM의 기본 동작은 다음에 비디오 스트림을 다시 만들 때까지(를 호출하여) 재생을 제한하지 않는 것입니다 `Netstream.stop()` 및 `Netstream.play()`).

소프트 강제 적용은 기본 비헤이비어이지만 다음 작업 중 하나를 수행하여 하드 강제 적용을 활성화할 수도 있습니다.

* 시간 제한이 만료되지 않았는지 확인하기 위해 비디오 플레이어에서 정기적으로 라이선스를 폴링하도록 합니다. 이 작업은 를 호출하여 수행할 수 있습니다. `DRMManager.loadVoucher(LOCAL_ONLY).` 오류 코드는 로컬에 저장된 라이선스가 더 이상 유효하지 않음을 나타냅니다.
* 사용자가 클릭할 때마다 **[!UICONTROL Pause]**, 현재 비디오 타임스탬프를 기록한 다음 를 호출할 수 있습니다. `Netstream.stop()`. 사용자가 재생 버튼을 클릭하면 기록된 위치를 찾은 다음 를 호출할 수 있습니다. `Netstream.play()`.