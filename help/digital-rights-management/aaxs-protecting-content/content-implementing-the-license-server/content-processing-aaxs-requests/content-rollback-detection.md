---
title: 롤백 감지
description: 롤백 감지
copied-description: true
exl-id: 525ae64e-1ade-4661-8403-ee4e42181358
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 롤백 감지{#rollback-detection}

롤백 감지를 위해 일부 사용 규칙은 클라이언트가 권한을 시행하기 위해 상태 정보를 유지 관리해야 합니다. 예를 들어 재생 창 사용 규칙을 적용하기 위해 클라이언트는 사용자가 콘텐츠를 처음 보기 시작한 날짜 및 시간을 저장합니다. 이 이벤트는 재생 창의 시작을 트리거합니다. 재생 창을 안전하게 적용하려면 서버는 클라이언트에 저장된 재생 창 시작 시간을 제거하기 위해 사용자가 클라이언트 상태를 백업 및 복원하지 않도록 해야 합니다. 서버는 클라이언트의 롤백 카운터 값을 추적하여 이를 수행합니다. 각 요청에 대해 서버는 를 호출하여 카운터 값을 가져옵니다. `RequestMessageBase.getClientState()` 을(를) 가져오려면 `ClientState` 객체, 호출 `ClientState.getCounter()` 클라이언트 상태 카운터의 현재 값을 가져옵니다. 서버는 각 클라이언트에 대해 이 값을 저장해야 합니다(사용 `MachineId.getUniqueId()` 를 눌러 롤백 카운터 값)과 연관된 클라이언트를 식별한 다음 `ClientState.incrementCounter()` 카운터 값을 1씩 늘립니다. 서버가 카운터 값이 서버에서 확인한 마지막 값보다 작음을 감지하면 클라이언트 상태가 롤백되었을 수 있습니다. 클라이언트 상태 변조 탐지에 대한 자세한 내용은 `ClientState` API 참조 설명서입니다.
