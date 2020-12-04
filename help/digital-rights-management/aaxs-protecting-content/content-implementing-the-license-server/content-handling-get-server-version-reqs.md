---
seo-title: 서버 버전 가져오기 요청 처리
title: 서버 버전 가져오기 요청 처리
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 서버 버전 가져오기 요청 처리{#handling-get-server-version-requests}

Adobe Access 클라이언트 3.0 이상에서는 서버 버전 가져오기 요청을 보내 서버의 기능을 확인합니다. Adobe 액세스 SDK 3.0 이상을 사용하는 모든 서버는 서버 버전 가져오기 요청에 대한 지원을 구현해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`입니다.
* 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/getServerVersion/v3&quot;이어야 합니다.

Adobe 액세스 SDK 4.0 이상의 경우 서버 버전 가져오기 요청에 대한 응답은 서버가 Adobe 액세스 프로토콜의 버전 3 및 4를 지원함을 클라이언트에 나타냅니다.
