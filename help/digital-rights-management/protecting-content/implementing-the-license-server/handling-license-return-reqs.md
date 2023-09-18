---
title: 라이선스 반환 요청 처리
description: 라이선스 반환 요청 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 라이선스 반환 요청 처리{#handle-license-return-requests}

클라이언트 애플리케이션이 라이센스를 반환해야 하는 경우 `DRMManager.returnVoucher()` 프로세스를 시작하는 Actionscript API입니다. 이 API는 다음에서 작동할 수 있습니다. `immediateCommit` 모드 또는 `confirmFirst` 모드. If `immediateCommit` 이(가) (으)로 설정됨 `true`그런 다음 클라이언트는 라이센스 반환 요청을 받았다는 라이센스 서버의 확인을 기다리지 않고 즉시 로컬 라이센스를 삭제합니다. Adobe Primetime DRM 라이센스 서버는 요청을 처리하고 클라이언트에 응답을 보내야 합니다. 라이선스 서버에서 지정된 사용자의 라이선스 수를 줄이는 등 요청을 처리하는지 여부는 라이선스 서버에 의해 결정됩니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

최소값 `Adobe Primetime DRM` 필요한 SDK 버전은 버전 5이고 요청 URL은 입니다. [!DNL /flashaccess/lreturn/v5]&quot;. 도메인 등록 취소와 마찬가지로 서버는 `getRequestPhase()` 클라이언트에서 라이센스 반환을 미리 볼 수 있는지 확인합니다.
