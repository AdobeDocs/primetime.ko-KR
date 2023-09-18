---
title: 라이선스를 발급할 때 컴퓨터 개수
description: 라이선스를 발급할 때 컴퓨터 개수
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 라이선스를 발급할 때 컴퓨터 개수{#machine-count-when-issuing-licenses}

비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이선스 서버 또는 도메인 서버는 사용자와 연결된 컴퓨터 ID를 저장해야 합니다. 시스템 ID를 추적하는 가장 강력한 방법은 가 반환하는 값을 저장하는 것입니다. `MachineId.getBytes()` 데이터베이스의 메서드입니다. 새 요청이 들어오면 를 사용하여 요청의 시스템 ID를 알려진 시스템 ID와 비교합니다. `MachineId.matches()`.

`MachineId.matches()` 는 ID를 비교하여 동일한 컴퓨터를 나타내는지 확인합니다. 이 비교는 비교할 컴퓨터 ID가 적은 경우에만 실용적입니다. 예를 들어, 사용자에게 도메인 내에 5개의 시스템이 허용된 경우 데이터베이스에서 사용자의 사용자 이름과 연결된 시스템 ID를 검색하고 비교할 작은 데이터 세트를 얻을 수 있습니다.

>[!NOTE]
>
>익명 액세스를 허용하는 배포에 대해서는 이 비교가 실용적이지 않습니다. 그러한 경우 `MachineId.getUniqueID()` 그러나 를 사용할 수 있지만 이 ID는 사용자가 Flash 및 Adobe AIR® 런타임 모두에서 콘텐츠에 액세스하는 경우 동일하지 않으며 사용자가 하드 드라이브를 다시 포맷하는 경우 유지되지 않습니다.

에 대해 자세히 알아보기 `MachineToken.getMachineId()`및 `MachineId.matches()`, 다음을 참조하십시오. *Adobe 액세스 API 참조*.
