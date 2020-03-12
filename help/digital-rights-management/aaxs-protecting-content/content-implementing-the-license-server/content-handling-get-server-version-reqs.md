---
seo-title: 서버 버전 가져오기 요청 처리
title: 서버 버전 가져오기 요청 처리
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 서버 버전 가져오기 요청 처리{#handling-get-server-version-requests}

Adobe Access 클라이언트 3.0 이상에서는 서버 버전 다운로드 요청을 보내 서버의 기능을 확인합니다. Adobe Access SDK 3.0 이상을 사용하는 모든 서버는 Get Server Version 요청에 대한 지원을 구현해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 요청 URL 파섹

Adobe Access SDK 4.0 이상의 경우 Get Server 버전 요청에 대한 응답은 서버가 Adobe Access 프로토콜의 버전 3 및 4를 지원한다는 것을 클라이언트에 알려 줍니다.
