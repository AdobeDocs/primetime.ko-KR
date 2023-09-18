---
title: 롤백 감지
description: 롤백 감지
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 롤백 감지 {#rollback-detection}

Adobe 액세스 구현에서 클라이언트가 상태(예: 재생 창 간격)를 유지해야 하는 비즈니스 규칙을 사용하는 경우, Adobe은 서버에서 롤백 카운터를 계속 추적하고 AIR 또는 SWF 허용 목록을 사용할 것을 강력히 권장합니다.

롤백 카운터는 클라이언트의 대부분의 요청에서 서버로 전송됩니다. Adobe 액세스 구현에서 롤백 카운터가 필요하지 않으면 무시할 수 있습니다. Adobe 그렇지 않으면 서버에서 를 사용하여 가져온 임의의 컴퓨터 ID를 저장하는 것이 좋습니다. `MachineToken.getMachineId().getUniqueId()`- 데이터베이스의 현재 카운터 값 롤백 카운터 증분 및 추적에 대한 자세한 내용은 *Adobe 액세스 API 참조* 및 *롤백 감지* 위치: *컨텐츠 보호를 위해 Adobe 액세스 SDK 사용*.
