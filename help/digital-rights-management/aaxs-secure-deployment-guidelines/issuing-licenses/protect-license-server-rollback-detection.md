---
seo-title: 롤백 감지
title: 롤백 감지
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 롤백 감지{#rollback-detection}

Adobe Access를 구현하면 클라이언트에서 상태를 유지해야 하는 비즈니스 규칙(예: 재생 창 간격)을 사용하는 경우 서버가 롤백 카운터를 추적하고 AIR 또는 SWF 화이트리스트를 사용하는 것이 좋습니다.

롤백 카운터는 클라이언트의 대부분의 요청에서 서버로 전송됩니다. Adobe Access 구현에 롤백 카운터가 필요하지 않으면 무시될 수 있습니다. 그렇지 않으면 서버가 데이터베이스에 있는 현재 카운터 값과 함께 `MachineToken.getMachineId().getUniqueId()`가져온 무작위 컴퓨터 ID를 저장하는 것이 좋습니다. 롤백 카운터 증분 및 추적에 대한 자세한 내용은 Adobe Access API 참조 및 컨텐츠 보호를 *위해 Adobe Access SDK* *를 사용하여* 롤백 *검색을*&#x200B;참조하십시오.
