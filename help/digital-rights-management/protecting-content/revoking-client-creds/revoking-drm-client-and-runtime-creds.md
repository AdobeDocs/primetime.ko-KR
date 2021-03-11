---
title: DRM 클라이언트 및 런타임 자격 증명 취소
description: DRM 클라이언트 및 런타임 자격 증명 취소
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# DRM 클라이언트 및 런타임 자격 증명 취소 {#revoking-drm-client-and-runtime-credentials}

DRM/런타임 버전은 보안 수준, 버전 번호 및 운영 체제 및 런타임을 비롯한 기타 특성에 의해 식별됩니다. 허용된 DRM/런타임 버전을 제한하려면 DRM 정책 또는 `HandlerConfiguration`에서 모듈 제한을 설정합니다. 모듈 제한에는 최소 보안 수준과 라이센스를 발급받을 수 없는 모듈 버전의 목록이 포함될 수 있습니다.

DRM/런타임 모듈을 식별하는 데 사용되는 특성에 대한 자세한 내용은 [보호된 내용](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md)에 액세스할 수 없는 DRM 클라이언트의 차단 목록을 참조하십시오.

최소 보안 수준이 설정된 경우 클라이언트 버전(컴퓨터 토큰에 지정됨)이 지정된 값보다 크거나 같아야 합니다.

제외된 버전 목록이 지정되어 있고 클라이언트의 버전이 목록의 버전 식별자와 일치하는 경우 클라이언트는 이 ModuleRequirements 인스턴스를 포함하는 권한을 사용할 수 없습니다. 모듈이 버전 정보와 일치하도록 하려면 릴리스 버전을 제외하고 버전 정보에 지정된 모든 매개 변수가 모듈 값과 정확히 일치해야 합니다. 릴리스 버전은 클라이언트 모듈의 값이 버전 정보의 값보다 작거나 같으면 일치합니다.

특정 DRM 클라이언트 또는 런타임 버전으로 위반이 보고되는 경우 컨텐츠 소유자 및 컨텐츠 배포자(라이선스 서버를 실행)는 Adobe에 수정 사항이 없는 기간 동안 서버 측에서 라이선스를 발급하지 않도록 구성할 수 있습니다. 위에서 설명한 바와 같이 `HandlerConfiguration`을 통해 또는 모든 DRM 정책을 변경하여 구성할 수 있습니다. 후자의 경우 DRM 정책 업데이트 목록을 유지 관리하고 이를 사용하여 DRM 정책이 업데이트되었는지 또는 해지되었는지 확인할 수 있습니다.

최신 버전의 Adobe Flash Player/Adobe AIR 런타임 또는 Adobe DRM 모듈(Content Protection Library)이 필요한 경우 DRM 정책을 업데이트해야 합니다.

Java API](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md)를 사용하여 정책 업데이트를 참조하십시오.[

그런 다음 `HandlerConfiguration.setRuntimeModuleRequirements()` 또는 `HandlerConfiguration.setDRMModuleRequirements()`을 호출하여 DRM 정책 업데이트 목록을 만들거나 `HandlerConfiguration`에서 제한을 설정해야 합니다. 사용자가 지정된 차단 목록이 활성화된 새 라이센스를 요청하면 라이센스를 발급하기 전에 최신 런타임과 라이브러리를 설치해야 합니다.

블록 목록 DRM 및 런타임 버전의 예를 보려면 [Java API를 사용하여 정책 업데이트 블록의 샘플 코드를 참조하십시오. 블록 목록 DRM 및 런타임 버전](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md)에 대한 예를 참조하십시오.
