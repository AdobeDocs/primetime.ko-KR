---
seo-title: DRMManager 클래스 개요 사용
title: DRMManager 클래스 개요 사용
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# DRMManager 클래스 사용 {#using-the-drmmanager-class}

이 `DRMManager` 클래스를 사용하여 애플리케이션의 라이선스 및 Primetime DRM 라이선스 서버 세션을 관리할 수 있습니다.

**라이선스 관리**

장치가 보호된 내용을 재생할 때마다 런타임은 컨텐츠를 보는 데 필요한 라이센스를 얻고 캐시합니다. 응용 프로그램이 컨텐츠를 로컬에 저장하고 라이센스를 통해 오프라인 재생을 허용하는 경우 사용자는 네트워크에 연결하지 않고도 응용 프로그램에서 컨텐츠를 볼 수 있습니다. 를 `DRMManager`사용하여 라이선스를 미리 캐시할 수 있습니다. 응용 프로그램은 컨텐츠를 보는 데 필요한 라이센스를 얻을 필요가 없습니다. 예를 들어, 애플리케이션이 미디어 파일을 다운로드한 다음 사용자가 여전히 온라인 상태일 때 라이센스를 얻을 수 있습니다.

라이선스를 미리 로드하려면 `DRMContentData` 개체를 사용하십시오. 이 `DRMContentData` 개체에는 라이센스를 제공할 수 있는 Primetime DRM 라이선스 서버의 URL이 포함되어 있으며 사용자 인증이 필요한지 여부를 설명합니다. 이 정보를 통해, 이 `DRMManager` 방법을 호출하여 라이센스를 얻고 캐시할 수 `loadVoucher()` 있습니다. 사전 로딩 라이선스 워크플로우는 오프라인 재생을 **&#x200B;위한 사전 로딩 라이선스에 대해 자세히 설명합니다.

**세션 관리**

또한 Primetime DRM 라이선스 서버에 대한 사용자를 인증하고 영구 세션을 관리할 `DRMManager` 수 있습니다. Primetime DRM 라이선스 서버와의 세션을 설정하려면 이 `DRMManager` 메서드를 `authenticate()` 호출하십시오. 인증이 성공적으로 완료되면 `DRMManager` 개체가 `DRMAuthenticationCompleteEvent` 전달됩니다. 이 개체에는 세션 토큰이 포함되어 있습니다. 이 토큰을 저장하여 사용자가 계정 자격 증명을 제공할 필요가 없도록 이후 세션을 설정할 수 있습니다. 토큰을 메서드에 전달하여 인증된 새 세션을 `setAuthenticationToken()` 설정합니다. 토큰을 생성한 서버의 설정에 따라 토큰 만료 및 기타 속성이 결정됩니다.

## DRMStatus 이벤트 처리 {#handling-drmstatus-events}

이 `DRMManager` 메서드는 `DRMStatusEvent` `loadVoucher()` 메서드 호출이 성공적으로 완료된 후 객체를 전달합니다. 라이센스를 받은 경우 이벤트 객체의 detail 속성에 값이 있습니다.바우처 `DRM.voucherObtained`속성에 `DRMVoucher` 개체가 포함됩니다. 라이센스를 취득하지 않은 경우 세부 정보 속성에 여전히 값이 있습니다.1. `DRM.voucherObtained`그러나 바우처 속성이 null입니다. 예를 들어, 사용자가 의 라이센스를 사용하고 로컬에 캐시된 라이선스가 없는 경우 라이선스를 얻을 수 `LoadVoucherSetting` 없습니다 `localOnly` . 인증 또는 통신 오류로 인해 호출이 성공적으로 완료되지 `loadVoucher()` 않으면 대신 `DRMManager``DRMErrorEvent` 또는 `DRMAuthenticationErrorEvent` 객체를 전달합니다.

## DRMAuthenticationComplete 이벤트 처리{#handling-drmauthenticationcomplete-events}

사용자가 `DRMManager` 메서드를 호출하여 성공적으로 인증되면 `DRMAuthenticationCompleteEvent` `authenticate()` 객체를 전달합니다. 이 `DRMAuthenticationCompleteEvent` 개체에는 응용 프로그램 세션에서 사용자 인증을 유지하는 데 사용할 수 있는 재사용 가능한 토큰이 포함되어 있습니다. 이 토큰을 `DRMManager` `setAuthenticationToken()` 방법으로 전달하여 세션을 다시 설정합니다. 토큰 작성자는 만료와 같은 토큰 특성을 설정합니다. Adobe는 토큰 속성을 검사하기 위한 API를 제공하지 않습니다.)

## DRMAuthenticationError 이벤트 처리{#handling-drmauthenticationerror-events}

사용자가 `DRMManager` 또는 `DRMAuthenticationErrorEvent` `authenticate()` `setAuthenticationToken()` 메서드를 호출하여 성공적으로 인증할 수 없을 때 객체를 전달합니다.