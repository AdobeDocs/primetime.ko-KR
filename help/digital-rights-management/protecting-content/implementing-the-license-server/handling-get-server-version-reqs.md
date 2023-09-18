---
title: 서버 버전 가져오기 요청 처리
description: 서버 버전 가져오기 요청 처리
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 서버 버전 가져오기 요청 처리 {#handle-get-server-version-requests}

Adobe Primetime DRM 클라이언트 3.0 이상은 서버 버전 가져오기 요청을 전송하여 서버의 기능을 확인합니다. Primetime DRM SDK 3.0 이상을 사용하는 모든 서버는 서버 버전 가져오기 요청에 대한 지원을 구현해야 합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;이어야 합니다. [!DNL /flashaccess/getServerVersion/v3]&quot;

Primetime DRM SDK 4.0 이상의 경우, 서버 버전 가져오기 요청에 대한 응답은 서버가 Primetime DRM 프로토콜 버전 3 및 4를 지원함을 클라이언트에 나타냅니다.
