---
title: 서버 버전 가져오기 요청 처리
description: 서버 버전 가져오기 요청 처리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 서버 버전 가져오기 요청 처리{#handling-get-server-version-requests}

Adobe Access 클라이언트 3.0 이상에서는 서버 기능을 결정하기 위해 Get Server 버전 요청을 보냅니다. Adobe Access SDK 3.0 이상을 사용하는 모든 서버는 서버 버전 가져오기 요청에 대한 지원을 구현해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`입니다.
* 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/getServerVersion/v3&quot;이어야 합니다.

Adobe Access SDK 4.0 이상의 경우 Get Server 버전 요청에 대한 응답은 서버가 Adobe 액세스 프로토콜 버전 3 및 4를 지원함을 클라이언트에 나타냅니다.
