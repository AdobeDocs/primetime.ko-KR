---
seo-title: 개요
title: 개요
uuid: 2bbf0aa1-df35-429d-84df-db357fa53e47
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 개요 {#overview}

고객은 라이센스를 얻기 위해 패키지된 컨텐츠에 포함된 메타데이터로부터 요청을 작성한 다음 해당 요청을 라이센스 서버에 제출합니다. 라이센스 서버는 컨텐츠 메타데이터에서 추출한 정보를 사용하여 라이센스를 생성합니다.

클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;입니다. 프로토콜 버전 3이 클라이언트 또는 서버에서 지원되는 최대 버전인 경우 Primetime DRM 클라이언트는 인증 요청을 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;로 보냅니다. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이센스 서버 URL&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;로 전송됩니다.

장치에 동일한 컨텐츠(동일한 라이센스 ID)에 대한 여러 개의 라이선스가 있을 수 있지만 특정 라이선스 ID 및 DRM 정책 ID에 대한 라이선스는 하나만 있을 수 있습니다. 중복된 LicenseID/PolicyID가 있는 라이센스를 받은 경우 새 라이센스는 새 라이센스의 발행일이 기존 라이센스의 발행일보다 늦은 경우에만 이전 라이센스를 대체합니다. 이 논리는 컨텐츠에 포함된 라이선스를 처리하는 데 사용됩니다. 따라서 동일한 DRM 정책 ID 파섹 ActionScript3 API를 통해 클라이언트에 전달되는 라이센스에는 동일한 논리가 `DRMManager.storeVoucher()` 적용됩니다.클라이언트가 이미 나중 발행일에 라이센스를 보유하고 있는 경우 제공된 라이센스가 무시될 수 있습니다.

## 라이선스 요청 처리 클래스 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - 라이센스 요청 처리기 클래스입니다. 라이센스 요청을 읽고 구문 분석합니다. 이 `getRequests()` 메서드는 `LicenseRequestMessage` 개체 목록을 반환합니다.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - 요청 메시지 클래스입니다. 호출자는 에서 반환된 `LicenseRequestMessage` 목록을 반복해야 `getRequests()`하며 각 요청에 대해 라이센스를 생성하거나 오류 코드를 설정해야 합니다. 콘텐트 ID, 라이선스 ID 및 DRM 정책을 포함하여 콘텐트 메타데이터에서 추출한 정보를 얻으려면 `LicenseRequestMessage.getContentInfo()` 호출을 참조하십시오.

라이선스 및 오류는 `LicenseHandler.close()` 메서드를 호출할 때 한 번에 전송됩니다.

자세한 내용은 [DRM Server API 참조 설명서를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 참조하십시오.
