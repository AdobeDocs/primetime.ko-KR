---
seo-title: 인증서 정보
title: 인증서 정보
uuid: 0b7818b4-bd6a-4f2e-94c2-565e0d735bf8
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 인증서 정보 {#about-certificates}

Adobe Primetime DRM SDK는 다음 구성으로 제공됩니다.

* Primetime DRM Production SDK
* Primetime DRM 평가 SDK
* Primetime DRM 시험버전 SDK

Primetime DRM SDK를 사용하여 라이선스 서버를 만들려면 Adobe에서 디지털 인증서를 얻어야 합니다. 디지털 인증서(인증서라고도 함)는 개인, 조직 또는 시스템과 같은 엔티티를 특정 공개 및 개인 키 쌍에 바인딩합니다. 디지털 인증서는 개인, 시스템 또는 조직의 ID를 확인하는 전자 자격 증명으로 간주할 수 있습니다.

배포 옵션에서 유연성을 극대화하고 보안을 강화하려면 Primetime DRM SDK에 다음 4개의 인증서가 필요합니다.

* 라이선스 서버 인증서

   SDK 파섹
* Packager 인증서

   SDK는 콘텐츠를 패키징(암호화)할 때 이 인증서를 사용하여 DRM 메타데이터를 생성합니다.
* 전송 인증서

   SDK 파섹
* 도메인 CA 인증서

   도메인 서버를 구현하려는 고객은 도메인 CA 인증서가 필요합니다. 다른 인증서와 달리 도메인 CA 인증서는 Adobe에서 발행하지 않습니다.

>[!NOTE]
>
>평가판 SDK 및 시험버전의 경우 라이선스 서버, 패키지 및 전송 인증서가 단일 인증서로 결합됩니다.

