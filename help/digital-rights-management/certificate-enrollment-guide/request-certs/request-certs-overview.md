---
seo-title: 인증서 요청 개요
title: 인증서 요청 개요
uuid: 3a4e79d7-1832-49d8-bcf2-a029b3729e6d
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 개요 {#request-certificates-overview}

Adobe Primetime DRM Production SDK를 사용하려면 다음 단계를 반복하여 각 인증서(라이센스 서버, 패키지 및 전송)를 요청합니다. 평가판 SDK 및 시험버전 SDK는 단일 인증서를 사용합니다.

>[!NOTE]
>
>이 문서에서 제공하는 예제에서는 OpenSSL을 사용합니다. 다른 유틸리티도 사용할 수 있습니다. 이러한 예는 참조용으로만 사용하십시오. HSM(Hardware Security Module)에 키 쌍 생성 및 키 및 인증서 저장에 대한 자세한 내용은 HSM에 대한 설명서를 참조하십시오.