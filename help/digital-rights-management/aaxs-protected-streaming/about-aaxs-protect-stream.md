---
title: 보호된 스트리밍을 위한 Adobe Access Server 정보
description: 보호된 스트리밍을 위한 Adobe Access Server 정보
copied-description: true
exl-id: 69fbc99d-ee1a-4066-ae01-d61838db32a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 보호된 스트리밍을 위한 Adobe Access Server 정보{#about-adobe-access-server-for-protected-streaming}

Protected Streaming용 Adobe® 액세스™ 서버는 Adobe 액세스 SDK를 기반으로 하는 라이센스 서버 구현입니다. 이 서버는 Adobe 액세스 클라이언트에 보호된 콘텐츠에 대한 라이선스를 발급합니다.

Adobe Access Server for Protected Streaming은 여러 테넌트를 지원합니다. 즉, 단일 서버를 여러 콘텐츠 게시자를 대신하여 호스팅할 수 있으며 각 서버는 자체 구성 설정을 가집니다. 또한 서버는 사용자 지정 인증 구성 요소를 지원하므로 라이선스를 발급하기 전에 사용자 지정 논리를 실행할 수 있습니다.

이 서버는 HTTP 스트리밍에 사용하기 위한 것입니다. 따라서 이 서버 구현은 Adobe 액세스에서 사용할 수 있는 모든 기능을 지원하지는 않습니다. 예를 들어, Protected Streaming용 Adobe Access Server은 사용자 인증 요청, 다중 정책, 도메인 바인딩 라이선스, 라이선스 체인 또는 동기화 메시지를 지원하지 않습니다.
