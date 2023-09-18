---
title: BEES 서버에서 SSL 구성
description: BEES 서버에서 SSL 구성
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# BEES 서버에서 SSL 구성 {#configure-ssl-on-your-bees-server}

1. 이 소프트웨어를 제공한 Adobe 담당자에게 서버 SSL 인증서를 제공합니다.

   이 인증서는 Primetime Cloud DRM 신뢰 저장소에 신뢰할 수 있는 인증서로 추가됩니다.
1. SSL 연결에 대해 클라이언트 인증을 활성화하려면(이 버전에서 비활성화됨):
   1. 추가 `[!DNL clouddrm-transport.cer]` 및 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 클라이언트 인증에 사용되는 신뢰 저장소에 인증서를 추가합니다.
   1. SSL 구성에서 클라이언트 인증을 활성화합니다.
