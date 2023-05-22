---
title: 개요
description: 개요
copied-description: true
exl-id: 267188d0-83f8-42dc-88e3-78b52945cb6c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 개요 {#overview}

라이센스를 얻기 위해 클라이언트는 패키지된 콘텐츠에 포함된 메타데이터에서 요청을 형성한 다음 해당 요청을 라이센스 서버에 제출합니다. 라이센스 서버는 라이센스 생성을 위해 콘텐츠 메타데이터로부터 추출된 정보를 사용한다.

클라이언트와 서버가 모두 프로토콜 버전 5를 지원하는 경우 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. 프로토콜 버전 3이 클라이언트나 서버에서 지원하는 최대값인 경우 Primetime DRM 클라이언트는 인증 요청을 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. 그렇지 않으면 인증 요청이 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;(으)로 전송됩니다 [!DNL /flashaccess/license/v1]&quot;

디바이스에는 동일한 콘텐츠(동일한 라이선스 ID)에 대한 여러 라이선스가 있을 수 있지만 특정 라이선스 ID 및 DRM 정책 ID에 대해서는 하나의 라이선스만 있을 수 있습니다. 중복 LicenseID/PolicyID가 있는 라이센스를 받은 경우 새 라이센스는 새 라이센스의 문제 일자가 기존 라이센스의 문제 일자 이후인 경우에만 이전 라이센스를 대체합니다. 이 논리는 콘텐츠에 포함된 라이선스를 처리하는 데 사용됩니다. 따라서 콘텐츠 청크에 동일한 DRM 정책 ID를 사용하는 두 개 이상의 라이선스를 임베드하지 않는 것이 좋습니다. 를 통해 클라이언트에 전달되는 라이센스에도 동일한 논리가 적용됩니다. `DRMManager.storeVoucher()` ActionScript3 API; 클라이언트가 나중에 발급하는 날짜가 포함된 라이선스를 이미 보유하고 있는 경우 제공된 라이선스를 무시할 수 있습니다.

## 라이선스 요청 처리 클래스 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - 라이선스 요청 처리기 클래스입니다. 라이선스 요청을 읽고 구문 분석합니다. 해당 `getRequests()` 메서드는 다음 목록을 반환합니다. `LicenseRequestMessage` 개체.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - 요청 메시지 클래스 호출자는 다음을 반복해야 합니다. `LicenseRequestMessage` 다음에 의해 반환된 목록 `getRequests()`, 그리고 각 요청에 대해 라이센스를 생성하거나 오류 코드를 설정합니다. 호출 `LicenseRequestMessage.getContentInfo()` 컨텐츠 ID, 라이선스 ID 및 DRM 정책을 포함하여 컨텐츠 메타데이터에서 추출된 정보를 가져옵니다.

다음과 같은 경우 라이센스 및 오류가 한 번에 전송됩니다. `LicenseHandler.close()` 메서드가 호출됩니다.

다음을 참조하십시오. [DRM 서버 API 참조 설명서](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 을 참조하십시오.
