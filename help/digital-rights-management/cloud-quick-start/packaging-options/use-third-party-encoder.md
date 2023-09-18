---
title: 서드파티 인코더 사용
description: 서드파티 인코더 사용
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 서드파티 인코더 사용{#use-a-third-party-encoder}

일부 고객은 하드웨어 또는 소프트웨어 비디오 인코더(또는 Adobe Media Server)를 사용하여 콘텐츠 준비 파이프라인을 이미 갖추고 있을 수 있습니다. 이 경우 현재 Primetime DRM 보호 콘텐츠를 만들 수 있는 모든 제품은 Primetime Cloud DRM 보호 키트와 동일한 구성 설정을 사용하여 Primetime Cloud DRM용 콘텐츠를 패키징할 수 있습니다. 키트에 포함된 기존 구성 파일 중 하나에서 필요한 정보를 얻을 수 있습니다. [!DNL config_hls.xml] 또는 [!DNL config_hds.xml].

관련 구성 항목은 다음과 같습니다.

* 라이선스 서버 URL
* 키 서버 URL
* 라이선스 서버 인증서
* 전송 인증서
