---
seo-title: 서버 버전 가져오기 요청 처리
title: 서버 버전 가져오기 요청 처리
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 서버 버전 가져오기 요청 처리 {#handle-get-server-version-requests}

Adobe Primetime DRM 클라이언트 3.0 이상이 서버 버전 가져오기 요청을 보내 서버의 기능을 확인합니다. Primetime DRM SDK 3.0 이상을 사용하는 모든 서버는 서버 버전 가져오기 요청에 대한 지원을 구현해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`입니다.
* 요청 메시지 클래스는 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`입니다.
* 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;이어야 합니다.

Primetime DRM SDK 4.0 이상 버전의 경우 서버 버전 가져오기 요청에 대한 응답은 서버가 Primetime DRM 프로토콜 3 및 4 버전을 지원한다는 점을 고객에게 알립니다.
