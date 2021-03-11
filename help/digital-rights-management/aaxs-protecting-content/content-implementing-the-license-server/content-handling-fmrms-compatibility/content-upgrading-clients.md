---
title: 클라이언트 업그레이드
description: 클라이언트 업그레이드
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 클라이언트 업그레이드 {#upgrading-clients}

FMRMS 1.x 클라이언트가 Adobe 액세스 서버에 접속하는 경우 서버가 클라이언트에 업그레이드를 요청해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`입니다.
* 요청 URL은 &quot;*1.x content*&quot;의 기본 URL + &quot;/edcws/services/urn:EDCLicenseService&quot;입니다.

   다른 Adobe 액세스 요청 핸들러와 달리 이 핸들러는 요청 정보에 대한 액세스 권한을 제공하지 않거나 응답 데이터를 설정할 필요가 없습니다. `FMRMSv1RequestHandler` 인스턴스를 만든 다음 `close()`을(를) 호출합니다.