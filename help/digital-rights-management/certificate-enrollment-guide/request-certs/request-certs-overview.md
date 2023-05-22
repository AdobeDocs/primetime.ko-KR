---
title: 요청 인증서 개요
description: 요청 인증서 개요
copied-description: true
exl-id: 4ecdc3be-7db3-494c-af9e-fd4d57b988e4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 개요 {#request-certificates-overview}

Adobe Primetime DRM 프로덕션 SDK를 사용하려면 다음 단계를 반복하여 각 인증서(라이센스 서버, 패키지 및 전송)를 요청합니다. Evaluation SDK와 체험판 SDK는 단일 인증서를 사용합니다.

>[!NOTE]
>
>이 문서에 제공된 예제는 OpenSSL을 사용합니다. 다른 유틸리티도 사용할 수 있습니다. 이 예제는 참조용으로만 사용하십시오. HSM(Hardware Security Module)에 키 쌍을 생성하고 키와 인증서를 저장하는 방법에 대한 자세한 내용은 HSM 설명서를 참조하십시오.
