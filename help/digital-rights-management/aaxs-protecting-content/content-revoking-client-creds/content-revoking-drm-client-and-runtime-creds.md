---
title: DRM 클라이언트 및 런타임 자격 증명 취소
description: DRM 클라이언트 및 런타임 자격 증명 취소
copied-description: true
exl-id: f39d6523-9215-49ec-bb3b-e60fe6690dca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# DRM 클라이언트 및 런타임 자격 증명 취소{#revoking-drm-client-and-runtime-credentials}

DRM/런타임 버전은 보안 수준, 버전 번호 및 OS 및 런타임을 포함한 기타 속성으로 식별됩니다. 허용되는 DRM/런타임 버전을 제한하려면 정책 또는 `HandlerConfiguration`. 모듈 제한에는 최소 보안 수준 및 라이센스를 발급할 수 없는 모듈 버전 목록이 포함될 수 있습니다. 다음을 참조하십시오 [보호된 콘텐츠에 대한 액세스가 제한되는 DRM 클라이언트 차단 목록](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) DRM/런타임 모듈을 식별하는 데 사용되는 속성에 대한 세부 사항입니다.

최소 보안 수준을 설정하면 클라이언트의 버전(컴퓨터 토큰에 지정됨)이 지정된 값보다 크거나 같아야 합니다.

제외된 버전 목록이 지정되어 있고 클라이언트 버전이 목록에 있는 버전 식별자와 일치하는 경우 클라이언트는 이 ModuleRequirements 인스턴스를 포함하는 권한을 사용할 수 없습니다. 모듈이 버전 정보와 일치하도록 하려면 버전 정보에 지정된 모든 매개 변수(릴리스 버전은 제외)가 모듈의 값과 정확히 일치해야 합니다. 릴리스 버전은 클라이언트 모듈의 값이 버전 정보에 있는 값보다 작거나 같은 경우 일치합니다.

특정 DRM 클라이언트 또는 런타임 버전에서 위반이 보고되는 경우 콘텐츠 소유자 및 콘텐츠 배포자(라이센스 서버를 실행하는 사용자)는 Adobe에 수정 사항이 없는 기간 동안 라이센스 발급을 거부하도록 서버를 구성할 수 있습니다. 다음을 통해 구성할 수 있습니다. `HandlerConfiguration` 위에서 설명한 대로, 또는 모든 정책을 변경함으로써. 후자의 경우 정책 업데이트 목록을 유지 관리하고 이 목록을 사용하여 정책이 업데이트되었는지 또는 취소되었는지 확인할 수 있습니다.

최신 버전의 Adobe® Flash® 플레이어/Adobe® AIR® 런타임 또는 Adobe 컨텐츠 보호 라이브러리(DRM 모듈)가 필요한 경우 [Java API를 사용하여 정책 업데이트](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) 및 정책 업데이트 목록을 만들거나 `HandlerConfiguration` 를 호출하여 `HandlerConfiguration.setRuntimeModuleRequirements()` 또는 `HandlerConfiguration.setDRMModuleRequirements()`. 사용자가 이러한 차단 목록이 활성화된 새 라이센스를 요청할 때 라이센스를 발급하려면 먼저 최신 런타임 및 라이브러리를 설치해야 합니다. DRM 및 런타임 버전을 나열하는 블록에 대한 예제는 의 샘플 코드를 참조하십시오. [Java API를 사용하여 정책 업데이트](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
