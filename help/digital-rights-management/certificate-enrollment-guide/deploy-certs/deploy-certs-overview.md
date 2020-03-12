---
seo-title: 인증서 배포 개요
title: 인증서 배포 개요
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 개요 {#deploy-certificates-overview}

Adobe Primetime DRM 속성 파일에 인증서를 추가하려면 개인 키를 사용하여 PKCS#7 파일을 PFX 파일로 변환하고 PEM 파일이나 DER 파일을 생성합니다.

* 자격 증명(인증서 및 개인 키)이 필요한 경우 Primetime DRM 명령줄 도구와 Adobe HTTP Dynamic Streaming Packager에 PFX 파일이 필요합니다. SDK, 참조 구현 및 보호된 스트리밍을 위한 Primetime DRM 서버는 PFX 파일을 수락할 수 있으며 HSM에 저장된 자격 증명을 사용할 수도 있습니다.
* 인증서만 필요한 경우 대부분의 Primetime DRM 구성 요소는 HSM의 PEM 파일, DER 파섹 또는 인증서를 사용할 수 있습니다. Adobe HTTP Dynamic Streaming Packager는 인증서에 대한 DER 파일만 허용합니다.