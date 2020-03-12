---
seo-title: DRM 정책 사용 개요
title: DRM 정책 사용 개요
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 개요 {#working-with-drm-policies-overview}

컨텐츠 제공업체는 Primetime DRM SDK를 사용하여 미디어 파일에 DRM 정책을 적용할 수 있습니다. 관리자는 정책 관리 API를 사용하여 DRM 정책을 만들고, 세부 사항을 보고, 업데이트할 수 있습니다.

A *`DRM policy`* 는 보안 설정, 인증 요구 사항 및 사용 권한을 포함하는 정보 모음입니다. 정책은 사용자가 컨텐츠를 볼 수 있는 방법을 정의합니다. DRM 정책, 암호화 및 서명을 통해 컨텐츠 제공업체는 컨텐츠의 배포 범위와 상관없이 컨텐츠를 제어할 수 있습니다.

DRM 정책은 라이센스 서버가 라이센스를 생성할 때 사용하는 템플릿 역할을 합니다. 클라이언트는 라이센스를 요청하기 전에 DRM 정책을 참조하여 클라이언트가 서버에 라이센스 요청을 하기 전에 사용자에게 인증을 요청해야 하는지 여부를 결정할 수도 있습니다.

Adobe Flash Media Server 또는 HTTP 서버를 사용하여 보호된 컨텐츠를 제공할 수 있습니다. 사용자는 Primetime DRM SDK로 구축한 맞춤형 플레이어에서 보호된 콘텐츠를 다운로드하여 재생할 수 있습니다.

DRM 정책은 클라이언트에 부여되는 하나 이상의 권한을 지정합니다. 일반적으로 DRM 정책에는 최소 DRM이 포함됩니다 *`Play Right`*. 여러 개의 재생 권한을 지정할 수도 있으며, 각각 다른 제한 사항이 있습니다. 클라이언트는 여러 개의 재생 권한이 있는 라이센스를 받으면 모든 제한 사항을 충족하는 첫 번째 라이센스를 사용합니다. 예를 들어 다른 플랫폼에 서로 다른 출력 보호 설정을 적용할 수 있습니다.

이 `CreatePolicyWithOutputProtection.java` 예제를 보여주는 샘플 코드는 참조 구현 명령줄 도구 [!DNL samples] 디렉토리에서 을 참조하십시오.

Primetime DRM 정책 관리 API를 사용하여 다음 작업을 완료할 수 있습니다.

* 정책 만들기 및 업데이트
* DRM 정책 세부 사항 보기
* DRM 정책 업데이트 목록 관리

Java *API에 대한 자세한 내용은 Primetime* DRM API 참조를 참조하십시오.

Primetime *DRM 정책 관리자에* 대한 자세한 내용은 Adobe Primetime DRM 참조 구현 사용 안내서를 참조하십시오.
