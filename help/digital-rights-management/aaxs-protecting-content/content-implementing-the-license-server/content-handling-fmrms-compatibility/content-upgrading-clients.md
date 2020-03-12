---
seo-title: 클라이언트 업그레이드
title: 클라이언트 업그레이드
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d

---


# 클라이언트 업그레이드{#upgrading-clients}

FMRMS 1.x 클라이언트가 Adobe Access 서버에 접속하는 경우 서버는 클라이언트에 업그레이드를 요청해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`입니다.
* 요청 URL은 &quot;*1.x 컨텐츠의*&#x200B;기본 URL&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;입니다.

   다른 Adobe Access 요청 처리기와 달리 이 처리기는 요청 정보에 대한 액세스를 제공하지 않거나 응답 데이터를 설정할 필요가 없습니다. 인스턴스의 인스턴스를 `FMRMSv1RequestHandler`만든 다음 `close()`