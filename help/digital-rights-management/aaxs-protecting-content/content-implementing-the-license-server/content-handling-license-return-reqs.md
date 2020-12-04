---
seo-title: 라이선스 반품 요청 처리
title: 라이선스 반품 요청 처리
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 라이선스 반품 요청 처리{#handling-license-return-requests}

클라이언트 응용 프로그램이 라이센스를 반환해야 하는 경우 DRMManager.returnVoucher() Actionscript API를 호출하여 프로세스를 시작합니다. 이 API는 immediateCommit 모드 또는 confirmFirst 모드에서 작동할 수 있습니다. immediateCommit가 true로 설정된 경우 클라이언트는 라이센스 반환 요청을 받은 라이센스 서버에서 확인을 기다리지 않고 즉시 로컬 라이센스를 삭제합니다. Adobe 액세스 라이센스 서버는 요청을 처리하고 클라이언트에 응답을 보내야 합니다. 라이센스 서버가 실제로 요청과 함께 어떤 작업을 수행하는지(예: 해당 사용자의 라이센스 카운트 감소) 여부는 라이센스 서버에 따라 결정됩니다.

* 요청 처리기 클래스는 com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler입니다.
* 요청 메시지 클래스는 com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage입니다.

필요한 최소 Adobe 액세스 SDK 버전은 버전 5입니다.요청 URL은 &quot; `/flashaccess/lreturn/v5`&quot;이 됩니다. 도메인 등록 해제와 마찬가지로, 서버는 `getRequestPhase()`을 사용하여 클라이언트가 라이센스 반환을 미리 보고 있는지 확인해야 합니다.
