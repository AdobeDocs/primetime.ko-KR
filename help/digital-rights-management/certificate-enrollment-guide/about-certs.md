---
title: 인증서 정보
description: 인증서 정보
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 인증서 정보 {#about-certificates}

Adobe Primetime DRM SDK는 다음 구성에서 사용할 수 있습니다.

* Primetime DRM 프로덕션 SDK
* Primetime DRM 평가 SDK
* Primetime DRM 체험판 SDK

Primetime DRM SDK를 사용하여 라이선스 서버를 만들려면 Adobe에서 디지털 인증서를 받아야 합니다. 디지털 인증서(인증서라고도 함)는 개인, 조직 또는 시스템과 같은 엔티티를 특정 공개 및 개인 키 쌍에 바인딩합니다. 디지털 인증서는 개인, 시스템 또는 조직의 신원을 확인하는 전자 인증서라고 할 수 있다.

배포 옵션에서 유연성과 향상된 보안을 최대한 활용하려면 Primetime DRM SDK에 다음 4개의 인증서가 필요합니다.

* 라이선스 서버 인증서

  SDK는 이 인증서를 사용하여 클라이언트에 발급된 콘텐츠 라이선스에 서명합니다.
* 패키지 인증서

  SDK는 콘텐츠를 패키징(암호화)할 때 이 인증서를 사용하여 DRM 메타데이터를 생성합니다.
* 전송 인증서

  SDK는 이 인증서를 사용하여 클라이언트와 라이선스 서버 간의 통신을 보호합니다.
* 도메인 CA 인증서

  도메인 서버를 구현하려는 고객은 도메인 CA 인증서가 필요합니다. 다른 인증서와 달리 도메인 CA 인증서는 Adobe에서 발급하지 않습니다.

>[!NOTE]
>
>Evaluation SDK 및 Trial SDK의 경우 라이선스 서버, 패키지 및 전송 인증서가 단일 인증서로 결합됩니다.
