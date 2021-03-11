---
title: DRMManager 클래스 개요 사용
description: DRMManager 클래스 개요 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# DRMManager 클래스 {#using-the-drmmanager-class} 사용

애플리케이션의 라이선스 및 Primetime DRM 라이선스 서버 세션을 관리하려면 `DRMManager` 클래스를 사용합니다.

**라이선스 관리**

장치가 보호된 내용을 재생할 때마다 런타임은 내용을 보는 데 필요한 라이센스를 입수하고 캐시합니다. 응용 프로그램에서 내용을 로컬로 저장하고 라이센스에서 오프라인 재생을 허용하는 경우 사용자는 네트워크에 연결하지 않고도 응용 프로그램에서 내용을 볼 수 있습니다. `DRMManager`을 사용하여 라이선스를 미리 캐시할 수 있습니다. 응용 프로그램은 컨텐츠를 보는 데 필요한 라이센스를 얻을 필요가 없습니다. 예를 들어, 사용자가 온라인 상태일 때 응용 프로그램에서 미디어 파일을 다운로드한 다음 라이센스를 얻을 수 있습니다.

라이센스를 미리 로드하려면 `DRMContentData` 개체를 사용합니다. `DRMContentData` 개체에는 라이선스를 제공할 수 있는 Primetime DRM 라이선스 서버의 URL이 포함되어 있으며 사용자 인증이 필요한지 여부를 설명합니다. 이 정보를 사용하여 `DRMManager` `loadVoucher()` 메서드를 호출하여 라이센스를 얻고 캐시할 수 있습니다. 라이선스 사전 로드 작업 과정은 *오프라인 재생을 위한 라이선스 사전 로드*&#x200B;에 자세히 설명되어 있습니다.

**세션 관리**

또한 `DRMManager`을(를) 사용하여 Primetime DRM 라이선스 서버에 사용자를 인증하고 영구 세션을 관리할 수도 있습니다. Primetime DRM 라이선스 서버와의 세션을 설정하려면 `DRMManager` `authenticate()` 메서드를 호출합니다. 인증이 성공적으로 완료되면 `DRMManager`은 `DRMAuthenticationCompleteEvent` 객체를 전달합니다. 이 객체에는 세션 토큰이 포함되어 있습니다. 사용자가 계정 자격 증명을 제공할 필요가 없도록 이 토큰을 저장하여 이후 세션을 설정할 수 있습니다. 토큰을 `setAuthenticationToken()` 메서드에 전달하여 인증된 새 세션을 설정합니다. 토큰을 생성한 서버의 설정에 따라 토큰 만료 및 기타 속성이 결정됩니다.

## DRMStatus 이벤트 처리 {#handling-drmstatus-events}

`DRMManager`은 `loadVoucher()` 메서드 호출이 성공적으로 완료된 후 `DRMStatusEvent` 객체를 전달합니다. 라이센스를 취득한 경우 이벤트 객체의 detail 속성에 값이 있습니다.`DRM.voucherObtained` 및 voucher 속성에 `DRMVoucher` 개체가 포함되어 있습니다. 라이센스를 얻지 못한 경우 세부 정보 속성에 여전히 값이 있습니다.`DRM.voucherObtained`;그러나 voucher 속성은 null입니다. 예를 들어 `localOnly`의 `LoadVoucherSetting`을(를) 사용하고 로컬에 캐시된 라이센스가 없는 경우 라이센스를 받을 수 없습니다. 인증 또는 통신 오류로 인해 `loadVoucher()` 호출이 성공적으로 완료되지 않으면 `DRMManager`은 대신 `DRMErrorEvent` 또는 `DRMAuthenticationErrorEvent` 객체를 전달합니다.

## DRMAuthenticationComplete 이벤트 처리{#handling-drmauthenticationcomplete-events}

`DRMManager`은 사용자가 `authenticate()` 메서드 호출을 통해 성공적으로 인증되면 `DRMAuthenticationCompleteEvent` 객체를 전달합니다. `DRMAuthenticationCompleteEvent` 개체에는 응용 프로그램 세션 간에 사용자 인증을 유지하는 데 사용할 수 있는 재사용 가능한 토큰이 포함되어 있습니다. 이 토큰을 `DRMManager` `setAuthenticationToken()` 메서드에 전달하여 세션을 다시 설정합니다. 토큰 작성자는 만료와 같은 토큰 특성을 설정합니다. Adobe에서는 토큰 속성을 검사하는 API를 제공하지 않습니다.)

## DRMAuthenticationError 이벤트 처리{#handling-drmauthenticationerror-events}

`DRMManager`은 `authenticate()` 또는 `setAuthenticationToken()` 메서드를 호출하여 사용자가 성공적으로 인증할 수 없을 때 `DRMAuthenticationErrorEvent` 객체를 전달합니다.