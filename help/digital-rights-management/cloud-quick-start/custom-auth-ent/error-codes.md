---
title: BEES 오류 코드
description: BEES 오류 코드
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# BEES 오류 코드 {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

BEES 확인 중에 오류가 발생하면 `DRMErrorEvent`이(가) 클라이언트에 반환됩니다. 이 이벤트의 속성을 분석하여 실패의 특성에 대한 세부 정보를 찾을 수 있습니다. 가능한 오류 코드의 하위 세트가 아래에 나열되어 있습니다.

| 오류 | 설명 |
|---|---|
| `3304:305` | 인증/인증 요청을 처리하려는 Primetime Cloud DRM의 일반 인증 오류입니다. 일반적으로 BEES 문제와 관련되지 않습니다. 이 오류가 일관되게 발생하는 경우 진단 정보와 함께 Primetime Cloud DRM 팀에 문제 티켓을 제출해야 합니다. |
| `3329:0` | 응용 프로그램 특정 오류(BEES 인증기에서). 하위 오류 코드가 반환되지 않으면 오류 텍스트에 문제 세부 정보가 표시됩니다. 예를 들어 응답을 구문 분석하는 문제가 있거나 BEES 서버에 연결할 수 없습니다. |
| `3329:<HTTP error code>` | 200 이외의 HTTP 응답이 BEES 서버에서 발행되었습니다. HTTP 오류 코드는 하위 오류 코드 필드에서 클라이언트에 반환됩니다. 구성 문제가 있거나 BEES 서버가 중단되었을 수 있습니다. |
| `3329:<x>` | BEES 서버는 라이센스 요청을 허용하지 않습니다. 하위 오류 코드와 오류 텍스트는 JSON 응답의 `error` 및 `errorText` 속성 내에서 BEES 서버에서 지정합니다. 이러한 유형의 응답은 오류로 간주되지 않고 BEES 서버로부터의 일반적인 거부 반응으로 간주해야 합니다. |