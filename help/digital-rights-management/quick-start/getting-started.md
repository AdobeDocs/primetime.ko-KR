---
title: 시작하기
description: 시작하기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# 시작하기 {#getting-started}

이 문서에서는 점진적 다운로드를 사용하여 콘텐츠를 배포하는 Adobe Primetime DRM 에코시스템과 라이선스 배포를 위한 안전한 스트리밍을 위한 Primetime DRM Server를 제공합니다. 각 단계에 대한 추가 세부 사항은 다음 안내서에서 제공됩니다.

* *Primetime DRM Server를 사용하여 콘텐츠 보호*
* *안전한 스트리밍을 위한 Primetime DRM 서버 사용*

보호된 스트리밍을 위한 Primetime DRM Server는 소스 코드가 포함되지 않은 최소 기능 서버입니다. 전체 Java 소스를 사용하는 수정 가능한 서버는 *Primetime DRM 참조 구현 사용* 안내서를 참조하십시오. *설정을 대신하여 참조 라이선스 서버를 설정하고 보호된 스트리밍을 위한 Primetime DRM 서버(라이센스 서버)* 단계를 배포하는 경우

## 사전 요구 사항 {#prerequisites}

시작하기 전에 다음 작업을 완료하십시오.

* Windows 또는 Linux 컴퓨터 2대 다운로드:

   * 한 대의 컴퓨터가 라이센스 서버가 됩니다.
   * 한 대의 컴퓨터가 Content Server가 됩니다.

* 두 컴퓨터 모두에 다음 응용 프로그램을 설치합니다.

   * Tomcat 6.0.18
   * Java 1.6

## 인증서 가져오기 {#obtain-certificates}

SDK 소프트웨어가 제공되면 지정된 회사 인증서 관리자는 Adobe Primetime DRM 인증서 등록 프로세스를 완료하라는 초대장을 받게 됩니다. 자세한 내용은 *Primetime DRM 인증서 등록 안내서*&#x200B;를 참조하십시오.

1. 관리자는 하나 이상의 개인을 지정하여 인증서 요청자로 행동합니다.
1. 인증서 요청자는 개인 키와 CSR을 생성합니다.
1. 요청자는 인증서 요청을 제출합니다.
1. 회사 관리자가 요청을 승인합니다.
1. Adobe 인증서 관리자가 제출을 확인합니다.
1. 요청자는 인증서를 받고, 인증서를 개인 키와 바인딩하고, 인증서를 배포합니다. 에 설명되어 있습니다.

   인증서 배포에 대한 자세한 내용은 *보호된 스트리밍을 위한 Adobe Primetime DRM 서버 배포* 안내서를 참조하십시오.
1. 각 인증서 유형에 대해 3-6단계를 완료해야 합니다.

   Primetime DRM 프로덕션 버전의 경우, 요청자는 2년간 유효합니다. 라이선스 서버, 패키지 및 전송 인증서에 대해 별도로 요청해야 합니다.

   Primetime DRM 평가 또는 시험판을 사용하는 고객은 1년 또는 90일 동안 각각 유효한 하나의 인증서만 필요합니다.