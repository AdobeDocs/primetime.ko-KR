---
title: 서버 버전 가져오기 요청 처리
description: 서버 버전 가져오기 요청 처리
copied-description: true
exl-id: 125b0111-17e9-4f6f-954b-6975048cd2fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 서버 버전 가져오기 요청 처리{#handling-get-server-version-requests}

Adobe 액세스 클라이언트 3.0 이상에서는 서버의 기능을 결정하기 위해 서버 버전 가져오기 요청을 보냅니다. Adobe 액세스 SDK 3.0 이상을 사용하는 모든 서버는 서버 버전 가져오기 요청에 대한 지원을 구현해야 합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* 요청 메시지 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* 요청 URL은 &quot;메타데이터의 라이선스 서버 URL&quot; + &quot;/flashaccess/getServerVersion/v3&quot;이어야 합니다.

Adobe 액세스 SDK 4.0 이상의 경우, 서버 버전 가져오기 요청에 대한 응답은 서버가 Adobe 액세스 프로토콜 버전 3 및 4를 지원함을 클라이언트에 나타냅니다.
