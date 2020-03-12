---
seo-title: 라이선스 반품 요청 처리
title: 라이선스 반품 요청 처리
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 반품 요청 처리{#handling-license-return-requests}

클라이언트 응용 프로그램이 라이센스를 반환해야 하는 경우 DRMManager.returnVoucher() Actionscript API를 호출하여 프로세스를 시작합니다. 이 API는 immediateCommit 모드 또는 confirmFirst 모드에서 작동할 수 있습니다. immediateCommit이 true로 설정된 경우 클라이언트는 라이센스 반환 요청을 받은 라이센스 서버에서 확인을 기다리지 않고 로컬 라이센스를 즉시 삭제합니다. Adobe Access 라이선스 서버는 요청을 처리하고 클라이언트에 응답을 보내야 합니다. 라이센스 서버가 실제로 요청과 함께 어떤 작업을 수행하는지(예: 해당 사용자에 대한 라이센스 수 감소) 결정하기 위해 라이센스 서버에 달렸습니다.

* 요청 처리기 클래스는 com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler입니다.
* 요청 메시지 클래스는 com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage입니다.

필요한 최소 Adobe Access SDK 버전은 버전 5입니다.요청 URL은 &quot; `/flashaccess/lreturn/v5`&quot;입니다. 도메인 등록 해제와 마찬가지로 서버는 클라이언트가 라이센스 반환을 미리 보고 `getRequestPhase()` 있는지 여부를 확인하는 데 사용해야 합니다.
