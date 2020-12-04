---
seo-title: 롤백 감지
title: 롤백 감지
uuid: ec124bac-a1d7-45be-bf09-a99d5eec5042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 롤백 감지 {#rollback-detection}

롤백 탐지의 경우 일부 사용 규칙은 클라이언트가 권한 적용을 위해 상태 정보를 유지해야 합니다. 예를 들어, 재생 창 사용 규칙을 적용하기 위해 클라이언트는 사용자가 처음 컨텐츠를 보기 시작한 날짜와 시간을 저장합니다. 이 이벤트는 재생 창의 시작을 트리거합니다. 재생 창을 안전하게 적용하려면 서버가 클라이언트 상태를 백업 및 복원하지 않고 클라이언트에 저장된 재생 창 시작 시간을 제거해야 합니다. 서버는 클라이언트의 롤백 카운터 값을 추적하여 이 작업을 수행합니다.

각 요청에 대해 서버는 `RequestMessageBase.getClientState()`을(를) 호출하여 `ClientState` 개체를 가져온 다음 `ClientState.getCounter()`를 호출하여 클라이언트 상태 카운터의 현재 값을 가져옵니다. 서버는 각 클라이언트에 대해 이 값을 저장해야 합니다(롤백 카운터 값과 연결된 클라이언트를 식별하려면 `MachineId.getUniqueId()` 사용). 그런 다음 `ClientState.incrementCounter()`을(를) 호출하여 카운터 값을 하나씩 증가시켜야 합니다. 서버가 카운터 값이 서버에서 마지막으로 본 값보다 작다는 것을 감지하면 클라이언트 상태가 롤백되었을 수 있습니다.

클라이언트 상태 변조 검색에 대한 자세한 내용은 `ClientState` API 참조 설명서를 참조하십시오.
