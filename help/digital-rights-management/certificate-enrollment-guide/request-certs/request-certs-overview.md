---
title: 인증서 요청 개요
description: 인증서 요청 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 개요 {#request-certificates-overview}

Adobe Primetime DRM Production SDK를 사용하려면 다음 단계를 반복하여 각 인증서(라이센스 서버, 패키지 및 전송)를 요청합니다. 평가 SDK 및 시험 SDK는 단일 인증서를 사용합니다.

>[!NOTE]
>
>이 문서에서 제공하는 예제에서는 OpenSSL을 사용합니다. 다른 유틸리티를 사용할 수도 있습니다. 이러한 예는 참조용으로만 사용하십시오. HSM(Hardware Security Module)에 키 쌍 생성, 키 및 인증서 저장에 대한 자세한 내용은 HSM에 대한 설명서를 참조하십시오.