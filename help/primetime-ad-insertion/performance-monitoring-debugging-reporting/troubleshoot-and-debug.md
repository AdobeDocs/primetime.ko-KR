---
title: 문제 해결 및 디버그
description: 문제 해결 및 디버그
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 문제 해결 및 디버그 {#troubleshooting-debugging}

Primetime Ad Insertion은 CDN 전송 오류, 광고 크리에이티브 오류 또는 클라이언트 연결 오류와 같은 비디오 전송의 모든 단계에서 발생할 수 있는 문제를 식별하고 진단하는 도구를 제공합니다.

Primetime Ad Insertion은 [Bootstrap API 매개 변수](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` 또는 `ptdebug=AdCall` 부트스트랩 URL로 로그는 HTTP 응답 헤더와 Primetime Ad Insertion 콘솔에 모두 출력됩니다. 이 매개 변수는 프로덕션 스트림이 아닌, 현지화된 테스트용으로만 사용됩니다. 자세한 정보 로깅이 활성화된 경우 메시지 유형에 대한 자세한 내용은 [자세한 로깅의 ptdebug 로깅 이벤트](verbose-logging.md#ptdebug-logging-events).

또한 Primetime Ad Insertion은 X-ADBE-AI-X1 헤더를 사용하여 모든 요청에 대한 성능 디버깅을 제공합니다. 이 헤더는 주어진 요청에 대한 성능 및 광고 삽입을 측정하는 데 사용할 수 있습니다. 이 요청 헤더는 자세한 로깅 활성화 여부에 관계없이 사용할 수 있습니다. 자세한 내용은 [자세한 정보 헤더: X-ADBE-PTAI-X1](debugging-headers.md).
