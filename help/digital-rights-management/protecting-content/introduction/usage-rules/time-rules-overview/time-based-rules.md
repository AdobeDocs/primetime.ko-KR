---
seo-title: 시간 기반 규칙 개요
title: 시간 기반 규칙 개요
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 시간 기반 규칙 {#time-based-rules}

Primetime DRM은 시간 기반의 라이선스 제한 사항을 &quot;원활하게 적용&quot;하고 있습니다. 비디오를 재생하는 동안 시간 권한이 만료되는 경우 Primetime DRM의 기본 동작은 다음 번에 비디오 스트림을 다시 만들 때까지 재생을 제한하지 않습니다(`Netstream.stop()` 및 `Netstream.play()` 호출).

소프트 적용이 기본 동작이지만 다음 작업 중 하나를 수행하여 하드 강제성을 활성화할 수도 있습니다.

* 비디오 플레이어에서 주기적으로 라이센스를 폴링하여 시간 제한 사항이 만료되지 않도록 하십시오. 이 작업은 `DRMManager.loadVoucher(LOCAL_ONLY).`을(를) 호출하여 수행할 수 있습니다. 오류 코드는 로컬에 저장된 라이센스가 더 이상 유효하지 않음을 나타냅니다.
* 사용자가 **[!UICONTROL Pause]**&#x200B;을(를) 클릭할 때마다 현재 비디오 타임스탬프를 기록한 다음 `Netstream.stop()`을(를) 호출할 수 있습니다. 사용자가 [재생] 단추를 클릭하면 녹음된 위치로 이동한 다음 `Netstream.play()`을 호출할 수 있습니다.