---
title: DRMManager 클래스 개요 사용
description: DRMManager 클래스 개요 사용
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# DRMManager 클래스 사용 {#using-the-drmmanager-class}

사용 `DRMManager` 클래스에서 응용 프로그램의 라이선스 및 Primetime DRM 라이선스 서버 세션을 관리합니다.

**라이선스 관리**

장치가 보호된 콘텐츠를 재생할 때마다 런타임은 콘텐츠를 보는 데 필요한 라이선스를 획득하고 캐시합니다. 애플리케이션이 로컬에 콘텐츠를 저장하고 라이선스가 오프라인 재생을 허용하는 경우 사용자는 네트워크 연결 없이 애플리케이션에서 콘텐츠를 볼 수 있습니다. 사용 `DRMManager`를 클릭하여 라이센스를 미리 캐시할 수 있습니다. 애플리케이션은 콘텐츠를 보는 데 필요한 라이센스를 획득할 필요가 없습니다. 예를 들어, 사용자가 온라인 상태에 있는 동안 애플리케이션이 미디어 파일을 다운로드한 다음 라이센스를 획득할 수 있습니다.

라이센스를 미리 로드하려면 `DRMContentData` 개체. 다음 `DRMContentData` 개체에는 라이선스를 제공할 수 있고 사용자 인증이 필요한지 여부를 설명하는 Primetime DRM 라이선스 서버의 URL이 포함되어 있습니다. 이 정보를 사용하여 `DRMManager` `loadVoucher()` 라이센스를 가져오고 캐시하는 방법입니다. 라이선스 미리 로드 워크플로는에 자세히 설명되어 있습니다. *오프라인 재생을 위한 라이선스 미리 로드*.

**세션 관리**

다음을 사용할 수도 있습니다 `DRMManager` Primetime DRM 라이센스 서버에 사용자를 인증하고 지속 세션을 관리합니다. 호출 `DRMManager` `authenticate()` Primetime DRM 라이센스 서버로 세션을 설정하는 방법. 인증이 완료되면 다음 작업을 수행할 수 있습니다. `DRMManager` 발송: `DRMAuthenticationCompleteEvent` 개체. 이 개체에는 세션 토큰이 포함되어 있습니다. 이 토큰을 저장하여 나중에 세션을 설정할 수 있으므로 사용자가 계정 자격 증명을 제공할 필요가 없습니다. 토큰을 로 전달 `setAuthenticationToken()` 새 인증된 세션을 설정하는 방법입니다. 토큰을 생성한 서버의 설정은 토큰 만료 및 기타 속성을 결정합니다.

## DRMStatus 이벤트 처리 {#handling-drmstatus-events}

다음 `DRMManager` 발송: `DRMStatusEvent` 호출 뒤에 개체 `loadVoucher()` 메서드가 성공적으로 완료되었습니다. 라이센스를 얻으면 이벤트 객체의 detail 속성에는 다음 값이 있습니다. `DRM.voucherObtained`및 바우처 속성은 `DRMVoucher` 개체. 라이선스를 얻지 않은 경우 세부 사항 속성에는 여전히 값이 있습니다. `DRM.voucherObtained`그러나 바우처 속성이 null입니다. 예를 들어 를 사용하는 경우 라이센스를 얻을 수 없습니다. `LoadVoucherSetting` / `localOnly` 그리고 로컬로 캐시된 라이선스가 없습니다. 다음과 같은 경우 `loadVoucher()` 인증 또는 통신 오류로 인해 호출이 완료되지 않았습니다. `DRMManager` 발송: `DRMErrorEvent` 또는 `DRMAuthenticationErrorEvent` 개체.

## DRMAuthenticationComplete 이벤트 처리{#handling-drmauthenticationcomplete-events}

다음 `DRMManager` 발송: `DRMAuthenticationCompleteEvent` 개체: 사용자가 호출을 통해 성공적으로 인증되는 경우 `authenticate()` 메서드를 사용합니다. 다음 `DRMAuthenticationCompleteEvent` 개체에는 애플리케이션 세션 간에 사용자 인증을 유지하는 데 사용할 수 있는 재사용 가능한 토큰이 포함되어 있습니다. 이 토큰 전달 대상 `DRMManager` `setAuthenticationToken()` 세션을 다시 설정하는 방법입니다. 토큰 생성자는 만료와 같은 토큰 속성을 설정합니다. Adobe은 토큰 특성을 검사하기 위한 API를 제공하지 않습니다.)

## DRMAuthenticationError 이벤트 처리{#handling-drmauthenticationerror-events}

다음 `DRMManager` 발송: `DRMAuthenticationErrorEvent` 개체:에 대한 호출을 통해 사용자를 성공적으로 인증할 수 없는 경우 `authenticate()` 또는 `setAuthenticationToken()` 메서드를 사용합니다.