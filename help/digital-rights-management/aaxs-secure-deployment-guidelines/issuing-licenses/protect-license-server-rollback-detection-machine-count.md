---
title: 라이선스 발급 시 시스템 개수
description: 라이선스 발급 시 시스템 개수
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 라이선스 발행 시 컴퓨터 수{#machine-count-when-issuing-licenses}

비즈니스 규칙에서 사용자의 컴퓨터 수를 추적해야 하는 경우 라이선스 서버 또는 도메인 서버는 사용자와 연관된 컴퓨터 ID를 저장해야 합니다. 컴퓨터 ID를 추적하는 가장 강력한 방법은 `MachineId.getBytes()` 메서드에서 반환된 값을 데이터베이스에 저장하는 것입니다. 새 요청이 들어오면 요청의 컴퓨터 ID를 `MachineId.matches()`을(를) 사용하여 알려진 컴퓨터 ID와 비교합니다.

`MachineId.matches()` ID 비교를 수행하여 동일한 컴퓨터를 나타내는지 확인합니다. 비교할 컴퓨터 ID가 적은 경우에만 이 비교가 실용적입니다. 예를 들어 도메인 내에서 5대의 컴퓨터가 허용되는 경우 데이터베이스를 검색하여 사용자의 사용자 이름과 연관된 시스템 ID를 검색하고 비교할 작은 데이터 세트를 얻을 수 있습니다.

>[!NOTE]
>
>이러한 비교는 익명 액세스를 허용하는 배포에는 적합하지 않습니다. 이 경우 `MachineId.getUniqueID()`을(를) 사용할 수 있지만 사용자가 Flash 및 Adobe AIR® 런타임 둘 다의 컨텐츠에 액세스하는 경우 이 ID는 동일하지 않으며, 사용자가 하드 드라이브를 다시 포맷하는 경우 이 ID는 유지되지 않습니다.

`MachineToken.getMachineId()`및 `MachineId.matches()`에 대한 자세한 내용은 *Adobe 액세스 API 참조*&#x200B;를 참조하십시오.
