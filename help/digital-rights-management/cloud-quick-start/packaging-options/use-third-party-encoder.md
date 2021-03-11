---
title: 타사 인코더 사용
description: 타사 인코더 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 타사 인코더 사용{#use-a-third-party-encoder}

일부 고객은 하드웨어 또는 소프트웨어 비디오 인코더(또는 Adobe Medium 서버)를 사용하여 이미 적절한 컨텐츠 준비 파이프라인을 사용하고 있을 수 있습니다. 이러한 경우 Primetime DRM으로 보호된 콘텐츠를 제작할 수 있는 모든 제품은 Primetime Cloud DRM 보호 키트와 동일한 구성 설정을 사용하여 Primetime Cloud DRM용 콘텐츠를 패키지화할 수 있습니다. 필요한 정보는 키트에 포함된 기존 구성 파일 중 하나에서 얻을 수 있습니다.[!DNL config_hls.xml] 또는 [!DNL config_hds.xml].

관련 구성 항목은 다음과 같습니다.

* 라이선스 서버 URL
* 키 서버 URL
* 라이선스 서버 인증서
* 전송 인증서

