---
seo-title: BEES 서버에서 SSL 구성
title: BEES 서버에서 SSL 구성
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# BEES 서버에서 SSL 구성 {#configure-ssl-on-your-bees-server}

1. 이 소프트웨어를 제공한 Adobe 담당자에게 서버 SSL 인증서를 제공합니다.

   인증서는 Primetime Cloud DRM 트러스트 저장소에 신뢰할 수 있는 인증서로 추가됩니다.
1. SSL 연결에 대한 클라이언트 인증을 활성화하려면(이 버전에서 사용 안 함):
   1. 클라이언트 인증에 사용되는 `[!DNL clouddrm-transport.cer]` 트러스트 저장소에 및 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 인증서를 추가합니다.
   1. SSL 구성에서 클라이언트 인증을 활성화합니다.
