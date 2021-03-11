---
title: 컴퓨터 식별자 사용
description: 컴퓨터 식별자 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 컴퓨터 식별자 사용{#using-machine-identifiers}

모든 Adobe 액세스 요청(FMRMS 호환성을 지원하는 요청 제외)은 개인화 중 클라이언트에 발급된 컴퓨터 토큰에 대한 정보를 포함합니다. 컴퓨터 토큰에는 개인화 중에 할당된 식별자인 컴퓨터 ID가 포함됩니다. 이 식별자를 사용하여 사용자가 라이선스를 요청했거나 도메인에 가입한 컴퓨터 수를 카운트합니다.

식별자를 사용하는 방법은 두 가지가 있습니다. `getUniqueId()` 메서드는 개별화하는 동안 장치에 할당된 문자열을 반환합니다. 데이터베이스에 문자열을 저장하고 식별자별로 검색할 수 있습니다. 그러나 사용자가 하드 드라이브를 다시 포맷하고 다시 식별하면 이 식별자가 변경됩니다. 이 식별자는 동일한 컴퓨터의 서로 다른 브라우저에 있는 Adobe® AIR®와 Adobe® Flash® Player 간에 다른 값을 갖습니다.

컴퓨터를 보다 정확하게 계산하려면 `getBytes()`을 사용하여 전체 식별자를 저장할 수 있습니다. 컴퓨터가 이전에 표시되었는지 확인하려면 사용자 이름에 대한 모든 식별자를 가져오고 `matches()`에 문의하여 일치하는 항목이 있는지 확인하십시오. `matches()` 메서드를 사용하여 `MachineId.getBytes`에서 반환된 값을 비교해야 하므로 이 옵션은 비교할 값이 적은 경우에만 실용적입니다(예: 특정 사용자와 연결된 컴퓨터).
