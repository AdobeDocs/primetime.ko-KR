---
seo-title: 시간 기반 규칙 개요
title: 시간 기반 규칙 개요
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 시간 기반 규칙 {#time-based-rules}

Primetime DRM은 시간 기반의 라이선스 제한 사항을 &quot;소프트 적용&quot;하여 사용하고 있습니다. 비디오를 재생하는 동안 시간이 만료되는 경우 Primetime DRM의 기본 동작은 다음에 비디오 스트림을 다시 만들 때까지 재생을 제한하지 `Netstream.stop()` 않는 것입니다(통화 및 `Netstream.play()`호출).

소프트 적용이 기본 동작이지만 다음 작업 중 하나를 수행하여 강제 수행을 활성화할 수도 있습니다.

* 비디오 플레이어에서 주기적으로 라이센스를 폴링하여 제한 시간이 만료되지 않도록 하십시오. 이 작업은 로컬로 저장된 라이센스가 더 `DRMManager.loadVoucher(LOCAL_ONLY).` 이상 유효하지 않음을 나타내는 오류 코드를 호출하여 수행할 수 있습니다.
* 사용자가 클릭할 때마다 **[!UICONTROL Pause]**&#x200B;현재 비디오 타임스탬프를 기록한 다음 호출할 수 `Netstream.stop()`있습니다. 사용자가 [재생] 단추를 클릭하면 레코딩된 위치를 찾은 다음 호출할 수 `Netstream.play()`있습니다.