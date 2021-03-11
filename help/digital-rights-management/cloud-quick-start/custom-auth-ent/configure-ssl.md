---
title: BEES 서버에서 SSL 구성
description: BEES 서버에서 SSL 구성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# BEES 서버 {#configure-ssl-on-your-bees-server}에 SSL 구성

1. 이 소프트웨어를 제공한 Adobe 담당자에게 서버 SSL 인증서를 제공하십시오.

   인증서가 Primetime Cloud DRM 트러스트 저장소에 신뢰할 수 있는 인증서로 추가됩니다.
1. SSL 연결에 대해 클라이언트 인증을 활성화하려면(이 버전에서 비활성화됨):
   1. 클라이언트 인증에 사용되는 신뢰 저장소에 `[!DNL clouddrm-transport.cer]` 및 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 인증서를 추가합니다.
   1. SSL 구성에서 클라이언트 인증을 활성화합니다.
