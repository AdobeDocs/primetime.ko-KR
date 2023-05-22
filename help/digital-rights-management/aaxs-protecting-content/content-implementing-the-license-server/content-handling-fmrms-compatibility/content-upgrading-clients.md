---
title: 클라이언트 업그레이드
description: 클라이언트 업그레이드
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 클라이언트 업그레이드{#upgrading-clients}

FMRMS 1.x 클라이언트가 Adobe 액세스 서버에 연결하는 경우 서버에서 클라이언트를 업그레이드하라는 메시지를 표시해야 합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* 요청 URL은 입니다.*1.x 콘텐츠의 기본 URL*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   다른 Adobe 액세스 요청 처리기와 달리 이 처리기는 요청 정보에 대한 액세스를 제공하지 않거나 응답 데이터를 설정해야 합니다. 의 인스턴스 만들기 `FMRMSv1RequestHandler`, 그런 다음 를 호출합니다. `close()`
