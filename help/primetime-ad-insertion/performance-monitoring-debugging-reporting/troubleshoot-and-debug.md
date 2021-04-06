---
title: 문제 해결 및 디버그
description: 문제 해결 및 디버그
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 문제 해결 및 디버그 {#troubleshooting-debugging}

Primetime Ad Insertion은 CDN 전달 오류, 크리에이티브 오류 또는 클라이언트 연결 오류와 같은 비디오 전달 모든 단계에서 발생할 수 있는 문제를 식별하고 진단하는 도구를 제공합니다.

Primetime Ad Insertion은 부트스트랩 URL에 대한 [Bootstrap API 매개 변수](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` 또는 `ptdebug=AdCall`을(를) 통해 자세한 로깅을 지원합니다. 로그는 HTTP 응답 헤더와 Primetime Ad Insertion 콘솔에 모두 출력됩니다. 이 매개 변수는 프로덕션 스트림이 아니라 로컬라이즈된 테스트용으로만 사용됩니다. 자세한 로깅(verbose logging)이 활성화된 경우 메시지 유형에 대한 자세한 내용은 자세한 로깅(verbose logging)](verbose-logging.md#ptdebug-logging-events)에서 [ptdebug 로깅 이벤트를 참조하십시오.

또한 Primetime Ad Insertion은 X-ADBE-AI-X1 헤더를 통해 모든 요청에 대한 성능 디버깅을 제공하며, 지정된 요청에 대한 성능 측정 및 광고 삽입 기능을 사용할 수 있습니다. 자세한 로깅 활성화 여부에 관계없이 이 요청 헤더를 사용할 수 있습니다. 자세한 내용은 [자세한 내용 헤더:X-ADBE-PTAI-X1](debugging-headers.md).
