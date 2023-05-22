---
title: DRM 정책 작업 개요
description: DRM 정책 작업 개요
copied-description: true
exl-id: 734d0be3-2abe-400c-bc34-00046ec52f4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 개요 {#working-with-drm-policies-overview}

컨텐츠 제공자는 Primetime DRM SDK를 사용하여 미디어 파일에 DRM 정책을 적용할 수 있습니다. 그런 다음 관리자는 정책 관리 API를 사용하여 DRM 정책을 만들고, 세부 정보를 보고, 업데이트할 수 있습니다.

A *`DRM policy`* 는 보안 설정, 인증 요구 사항 및 사용 권한을 포함하는 정보의 모음입니다. 정책은 사용자가 콘텐츠를 보는 방법을 정의합니다. DRM 정책, 암호화 및 서명을 통해 콘텐츠 제공자는 콘텐츠가 아무리 널리 배포되더라도 콘텐츠를 계속 제어할 수 있습니다.

DRM 정책은 라이센스 서버가 라이센스를 생성할 때 사용하는 템플릿 역할을 합니다. 클라이언트는 또한 라이센스를 요청하기 전에 DRM 정책을 참조하여 클라이언트가 라이센스 요청을 서버에 발행하기 전에 사용자에게 인증을 요청해야 하는지 여부를 결정할 수 있습니다.

Adobe Flash Media Server 또는 HTTP 서버를 사용하여 보호된 콘텐츠를 제공할 수 있습니다. 사용자는 Primetime DRM SDK로 빌드된 사용자 지정 플레이어에서 보호된 콘텐츠를 다운로드하고 재생할 수 있습니다.

DRM 정책은 클라이언트에 부여된 하나 이상의 권한을 지정합니다. 일반적으로 DRM 정책은 최소한 다음을 포함합니다. *`Play Right`*. 각각 제한 사항이 다른 여러 재생 권한을 지정할 수도 있습니다. 클라이언트가 여러 재생 권한이 있는 라이선스를 받으면 모든 제한 사항을 충족하는 첫 번째 라이선스를 사용합니다. 예를 들어 플랫폼마다 다른 출력 보호 설정을 적용할 수 있습니다.

다음을 참조하십시오 `CreatePolicyWithOutputProtection.java` 참조 구현 명령줄 도구 [!DNL samples] 이 예제를 보여 주는 샘플 코드의 디렉토리.

Primetime DRM 정책 관리 API를 사용하여 다음 작업을 완료할 수 있습니다.

* 정책 생성 및 업데이트
* DRM 정책 세부 정보 보기
* DRM 정책 업데이트 목록 관리

다음을 참조하십시오. *Primetime DRM API 참조* Java API에 대한 자세한 내용.

다음을 참조하십시오. *Primetime DRM 참조 구현 사용* Primetime DRM 정책 관리자에 대한 자세한 내용은 안내서를 참조하십시오.
