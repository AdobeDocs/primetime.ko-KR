---
title: 라이선스 반환 요청 처리
description: 라이선스 반환 요청 처리
copied-description: true
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 라이선스 반환 요청 처리{#handling-license-return-requests}

클라이언트 애플리케이션이 라이센스를 반환해야 하는 경우 DRMManager.returnVoucher() Actionscript API를 호출하여 프로세스를 시작합니다. 이 API는 immediateCommit 모드 또는 confirmFirst 모드에서 작동할 수 있습니다. immediateCommit이 true로 설정되면 클라이언트는 라이센스 반환 요청을 받은 라이센스 서버의 확인을 기다리지 않고 즉시 로컬 라이센스를 삭제합니다. Adobe 액세스 라이선스 서버는 요청을 처리하고 클라이언트에 응답을 보내야 합니다. 라이선스 서버가 실제로 요청을 사용하여 어떤 작업도 수행하는지(예: 주어진 사용자에 대한 라이선스 수 감소) 여부는 라이선스 서버가 결정하는 바에 따라 결정됩니다.

* 요청 처리기 클래스는 com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler입니다
* 요청 메시지 클래스는 com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage입니다

필요한 최소 Adobe 액세스 SDK 버전은 버전 5입니다. 요청 URL은 &quot; `/flashaccess/lreturn/v5`&quot;. 도메인 등록 취소와 마찬가지로 서버는 `getRequestPhase()` 클라이언트에서 라이센스 반환을 미리 보고 있는지 확인합니다.
