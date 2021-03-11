---
description: 컨텐츠 패키징으로 인한 DASH 컨텐츠를 재생하려면 TVSDK 클라이언트가 키 획득 워크플로우의 패키징 프로세스 동안 전달된 컨텐츠 암호 해독 키를 입수해야 합니다. 클라이언트 컨텐츠 암호 해독 키는 일반적으로 클라이언트에서 하나 이상의 HTTP/HTTPS 게시물에 대한 응답으로 Widevine/PlayReady 라이센스 서버가 클라이언트에 전달합니다.
title: 클라이언트 키 요청 워크플로우 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 클라이언트 키 요청 워크플로 {#client-key-request-workflow-overview}

컨텐츠 패키징으로 인한 DASH 컨텐츠를 재생하려면 TVSDK 클라이언트가 키 획득 워크플로우의 패키징 프로세스 동안 전달된 컨텐츠 암호 해독 키를 입수해야 합니다. 클라이언트 컨텐츠 암호 해독 키는 일반적으로 클라이언트에서 하나 이상의 HTTP/HTTPS 게시물에 대한 응답으로 Widevine/PlayReady 라이센스 서버가 클라이언트에 전달합니다.

컨텐츠 암호 해독 키를 가져오려면 PSDK 클라이언트가 다음을 수행해야 합니다.

* 컨텐츠의 패치 상자를 선택하고 플랫폼에 제공한 다음 키 요청에 응답하여 얻습니다.
* HTTP POST을 통해 키 요청을 해당 Widevine/PlayReady 라이선스 서버로 보냅니다.
* 응답에서 클라이언트 컨텐츠 암호 해독 키를 추출하고 컨텐츠 암호 해독에 사용할 플랫폼에 서버 응답을 전달합니다.

키 요청에 대한 HTTP POST을 전송하려면 코드를 게시물에 연결해야 하는 추가 데이터와 함께 라이센스 서버 URL을 PSDK 클라이언트에 전달해야 합니다. 전달할 URL과 데이터 선택은 함께 작업하는 Widevine/PlayReady 서비스 공급자에 따라 달라집니다. 예를 들어 ExpressPlay를 사용하여 서비스를 제공하는 경우 적절한 ExpressPlay Widevin/PlayReady 라이선스 서버 URL을 전달하여 컨텐츠의 암호화 키와 연관된 ExpressPlay 토큰을 보내는 키 요청에 연결합니다. ExpressPlay 설명서에서 해당 ExpressPlay Widevine/PlayReady 라이센스 서버 URL을 확인할 수 있습니다.