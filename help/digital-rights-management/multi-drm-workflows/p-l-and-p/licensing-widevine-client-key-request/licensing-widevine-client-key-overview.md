---
description: 콘텐츠 패키징으로 인한 DASH 콘텐츠를 재생하려면, TVSDK 클라이언트는 키 획득 워크플로우에서 패키징 프로세스 중에 전달된 콘텐츠 암호 해독 키를 획득해야 합니다. 클라이언트 콘텐츠 암호 해독 키는 일반적으로 클라이언트로부터의 하나 이상의 HTTP/HTTPS 게시물에 대한 응답으로 Widevine/PlayReady 라이센스 서버에 의해 클라이언트에 전달됩니다.
title: 클라이언트 키 요청 워크플로 개요
exl-id: ae600cbd-415b-441a-bf01-f259993071f2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 클라이언트 키 요청 워크플로 {#client-key-request-workflow-overview}

콘텐츠 패키징으로 인한 DASH 콘텐츠를 재생하려면, TVSDK 클라이언트는 키 획득 워크플로우에서 패키징 프로세스 중에 전달된 콘텐츠 암호 해독 키를 획득해야 합니다. 클라이언트 콘텐츠 암호 해독 키는 일반적으로 클라이언트로부터의 하나 이상의 HTTP/HTTPS 게시물에 대한 응답으로 Widevine/PlayReady 라이센스 서버에 의해 클라이언트에 전달됩니다.

콘텐츠 암호 해독 키를 획득하려면 PSDK 클라이언트는 다음을 수행해야 합니다

* 콘텐츠의 pssh 상자를 가져와서 플랫폼에 제공하고 이에 대한 응답으로 주요 요청을 받습니다.
* HTTP POST을 통해 키 요청을 적절한 Widevine/PlayReady 라이선스 서버에 보냅니다.
* 응답에서 클라이언트 콘텐츠 암호 해독 키를 추출할 플랫폼에 서버의 응답을 전달하여 콘텐츠 암호 해독에 사용합니다.

키 POST에 대한 HTTP 요청을 전송하려면 코드는 POST에 첨부해야 하는 추가 데이터와 함께 라이선스 서버 URL을 PSDK 클라이언트에 전달해야 합니다. 전달할 URL 및 데이터는 함께 작업하는 Widevine/PlayReady 서비스 공급자에 따라 다릅니다. 예를 들어 ExpressPlay를 사용하여 서비스를 제공하는 경우 적절한 ExpressPlay Widevine/PlayReady 라이선스 서버 URL을 전달하고 콘텐츠의 암호화 키와 연결된 ExpressPlay 토큰을 발신 키 요청에 연결합니다. ExpressPlay 설명서에서 적절한 ExpressPlay Widevine/PlayReady 라이선스 서버 URL을 가져올 수 있습니다.
