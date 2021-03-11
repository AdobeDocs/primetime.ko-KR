---
title: 라이선스 반품 요청 처리
description: 라이선스 반품 요청 처리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 라이선스 반환 요청 처리{#handle-license-return-requests}

클라이언트 응용 프로그램이 라이센스를 반환해야 하는 경우 `DRMManager.returnVoucher()` Actionscript API를 호출하여 프로세스를 시작합니다. 이 API는 `immediateCommit` 모드 또는 `confirmFirst` 모드에서 작동할 수 있습니다. `immediateCommit`이(가) `true`로 설정된 경우 클라이언트는 라이센스 반환 요청을 받은 라이센스 서버에서 확인을 기다리지 않고 즉시 로컬 라이센스를 삭제합니다. Adobe Primetime DRM 라이선스 서버는 요청을 처리하고 클라이언트에 응답을 보내야 합니다. 라이센스 서버가 요청을 처리하는지 여부(예: 지정된 사용자의 라이선스 카운트 감소)는 라이선스 서버에 의해 결정됩니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`입니다.

필요한 최소 `Adobe Primetime DRM` SDK 버전은 버전 5;요청 URL은 &quot; [!DNL /flashaccess/lreturn/v5]&quot;입니다. 도메인 등록 제거 시 서버는 `getRequestPhase()`을 사용하여 클라이언트가 라이센스 반환을 미리 볼 수 있는지 여부를 결정합니다.
