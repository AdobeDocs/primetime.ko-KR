---
title: BEES 오류 코드
description: BEES 오류 코드
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# BEES 오류 코드 {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

BEES 검사 중에 오류가 발생하면 `DRMErrorEvent` 가 클라이언트에 반환됩니다. 이 이벤트의 속성을 구문 분석하여 실패의 특성에 대한 세부 정보를 찾을 수 있습니다. 가능한 오류 코드의 하위 집합은 아래에 나와 있습니다.

| 오류 | 설명 |
|---|---|
| `3304:305` | 인증/권한 부여 요청을 처리하려고 하는 Primetime Cloud DRM의 일반 권한 부여 오류입니다. 일반적으로 BEES 문제와 관련이 없습니다. 이 오류가 지속적으로 발생하면 진단 정보와 함께 문제 티켓을 Primetime Cloud DRM 팀에 제출해야 합니다. |
| `3329:0` | 애플리케이션별 오류(BEES 승인자). 하위 오류 코드가 반환되지 않으면 오류 텍스트에 문제에 대한 세부 정보가 표시됩니다. 예를 들어 응답을 구문 분석하는 도중 문제가 발생했거나 BEES 서버에 연결할 수 없습니다. |
| `3329:<HTTP error code>` | BEES 서버에서 200 이외의 HTTP 응답을 발행했습니다. HTTP 오류 코드는 하위 오류 코드 필드의 클라이언트에 반환됩니다. 이는 구성 문제 또는 BEES 서버 중단을 나타낼 수 있습니다. |
| `3329:<x>` | BEES 서버가 라이선스 요청을 허용하지 않았습니다. 하위 오류 코드 및 오류 텍스트는 JSON 응답 내의 BEES 서버에 의해 지정됩니다. `error` 및 `errorText` 속성. 이러한 종류의 응답은 오류로 간주되지 않고 BEES 서버의 정기적인 거부 응답이어야 합니다. |
