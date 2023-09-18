---
title: 시작
description: 시작
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 시작 {#getting-started}

이 문서에서는 점진적 다운로드를 사용하여 콘텐츠를 배포하는 Adobe Primetime DRM 생태계와 라이선스 배포를 위한 보호된 스트리밍용 Primetime DRM Server를 빠르게 설정하고 배포하는 단계를 제공합니다. 각 단계에 대한 자세한 내용은 다음 안내서에 나와 있습니다.

* *Primetime DRM 서버를 사용하여 콘텐츠 보호*
* *보호된 스트리밍에 Primetime DRM 서버 사용*

Primetime DRM Server for Protected Streaming은 소스 코드를 포함하지 않는 최소 기능 서버입니다. 전체 Java 소스가 있는 수정 가능한 서버의 경우 *Primetime DRM 참조 구현 사용* 가이드. 참조 라이선스 서버를 설정하면 이(가) *보호 스트리밍용 Primetime DRM 서버 설정 및 배포(라이센스 서버)* 단계.

## 전제 조건 {#prerequisites}

시작하기 전에 다음 작업을 완료하십시오.

* Windows 또는 Linux 컴퓨터 2대:

   * 하나의 컴퓨터가 라이센스 서버가 됩니다.
   * 한 대의 컴퓨터가 Content Server가 됩니다.

* 두 컴퓨터에 다음 응용 프로그램을 설치합니다.

   * Tomcat 6.0.18
   * Java 1.6

## 인증서 받기 {#obtain-certificates}

SDK 소프트웨어가 게재되면 지정된 회사 인증서 관리자는 Adobe Primetime DRM 인증서 등록 프로세스를 완료하라는 초대장을 받게 됩니다. 자세한 내용은 *Primetime DRM 인증서 등록 안내서*.

1. 관리자는 최소 한 명의 개인을 인증서 요청자로 지정합니다.
1. 인증서 요청자는 개인 키 및 CSR을 생성합니다.
1. 요청자가 인증서 요청을 제출합니다.
1. 회사 관리자가 요청을 승인합니다.
1. Adobe 인증서 관리자가 제출을 확인합니다.
1. 요청자가 인증서를 받고 개인 키로 인증서를 바인딩한 다음 인증서를 배포합니다. 에 설명된 대로

   인증서 배포에 대한 자세한 내용은 *보호된 스트리밍을 위해 Adobe Primetime DRM 서버 배포* 가이드.
1. 각 인증서 유형에 대해 3~6단계를 완료해야 합니다.

   Primetime DRM 프로덕션 버전의 경우 요청자는 2년 동안 유효한 라이센스 서버, 패키징 및 전송 인증서를 별도로 요청해야 합니다.

   Primetime DRM 평가 또는 체험판 버전을 사용하는 고객은 각각 1년/90일 동안 유효한 하나의 인증서만 있으면 됩니다.
