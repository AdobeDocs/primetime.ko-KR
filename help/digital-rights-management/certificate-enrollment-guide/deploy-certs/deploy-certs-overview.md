---
title: 인증서 배포 개요
description: 인증서 배포 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 개요 {#deploy-certificates-overview}

Adobe Primetime DRM 속성 파일에 인증서를 추가하려면 개인 키를 사용하여 PKCS#7 파일을 PFX 파일로 변환하고 PEM 파일 또는 DER 파일을 생성합니다.

* 자격 증명(인증서 및 개인 키)이 필요한 경우 Primetime DRM 명령줄 도구 및 Adobe HTTP Dynamic Streaming 패키지에는 PFX 파일이 필요합니다. 보호 스트리밍용 SDK, 참조 구현 및 Primetime DRM 서버는 PFX 파일을 수락할 수 있으며, HSM에 저장된 자격 증명을 사용할 수도 있습니다.
* 인증서만 필요한 경우 대부분의 Primetime DRM 구성 요소는 PEM 파일, DER 파일 또는 HSM의 인증서를 사용할 수 있습니다. Adobe HTTP Dynamic Streaming 패키저는 인증서에 대한 DER 파일만 허용합니다.
