---
seo-title: DRM 클라이언트 및 런타임 자격 증명 취소
title: DRM 클라이언트 및 런타임 자격 증명 취소
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# DRM 클라이언트 및 런타임 자격 증명 취소{#revoking-drm-client-and-runtime-credentials}

DRM/런타임 버전은 보안 수준, 버전 번호 및 OS 및 런타임을 비롯한 기타 속성으로 식별됩니다. 허용된 DRM/런타임 버전을 제한하려면 정책 또는 DPS에서 모듈 제한을 설정합니다 `HandlerConfiguration`. 모듈 제한 사항에는 최소 보안 수준과 라이센스를 발급받을 수 없는 모듈 버전 목록이 포함될 수 있습니다. DRM/ [런타임 모듈을 식별하는 데 사용되는 특성에 대한 자세한 내용은 보호된 콘텐츠에](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) 액세스할 수 없도록 제한된 DRM 클라이언트 차단 목록을 참조하십시오.

최소 보안 수준이 설정된 경우 클라이언트(컴퓨터 토큰에 지정됨)의 버전이 지정된 값보다 크거나 같아야 합니다.

제외된 버전의 목록이 지정되고 클라이언트의 버전이 목록의 버전 식별자와 일치하는 경우, 클라이언트는 이 ModuleRequirements 인스턴스를 포함하는 권한을 사용할 수 없습니다. 모듈이 버전 정보와 일치하도록 하려면 릴리스 버전을 제외하고 버전 정보에 지정된 모든 매개 변수가 모듈 값과 정확히 일치해야 합니다. 릴리스 버전은 클라이언트 모듈 값이 버전 정보의 값보다 작거나 같은 경우에 일치합니다.

특정 DRM 클라이언트 또는 런타임 버전으로 위반이 보고되는 경우, Adobe에서 수정 사항을 제공하지 않는 기간 동안 컨텐츠 소유자 및 컨텐츠 배포자(라이센스 서버를 실행)가 라이센스를 발급하지 않도록 서버를 구성할 수 있습니다. 위에 설명된 `HandlerConfiguration` 대로 또는 모든 정책을 변경하여 구성할 수 있습니다. 후자의 경우 정책 업데이트 목록을 유지 관리하고 이를 사용하여 정책이 업데이트되었는지 또는 해지되었는지 확인할 수 있습니다.

최신 버전의 Adobe® Flash® Player/Adobe® AIR® 런타임 또는 Adobe DRM 모듈(Content Protection Library)이 필요한 경우 Java API를 사용하여 정책 [업데이트](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) 및 정책 업데이트 목록 만들기에 나와 있는 대로 정책을 업데이트하거나, 호출 `HandlerConfiguration` 또는 `HandlerConfiguration.setRuntimeModuleRequirements()` `HandlerConfiguration.setDRMModuleRequirements()`로 제한 사항을 설정합니다. 사용자가 이러한 블록 목록이 활성화된 새로운 라이센스를 요청하면 라이센스를 발급하기 전에 최신 런타임과 라이브러리를 설치해야 합니다. DRM 및 런타임 버전 목록 블록의 예제는 Java API를 사용하여 정책 [업데이트의 샘플 코드를 참조하십시오](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
