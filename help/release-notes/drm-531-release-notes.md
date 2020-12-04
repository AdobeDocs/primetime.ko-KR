---
title: DRM 5.3.1 릴리스 노트
seo-title: DRM 5.3.1 릴리스 노트
description: DRM 5.3.1 릴리스 노트는 DRM 5.3.1의 새로운 기능과 알려진 문제를 설명합니다.
seo-description: DRM 5.3.1 릴리스 노트는 DRM 5.3.1의 새로운 기능과 알려진 문제를 설명합니다.
uuid: bb61b79f-a5b3-42ed-8016-495b1ac99ea6
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# DRM 5.3.1 릴리스 노트 {#drm-release-notes}

DRM 5.3.1 릴리스 노트는 DRM 5.3.1의 새로운 기능과 알려진 문제를 설명합니다.

## 버전 5.3 {#new-features}의 새로운 기능

* **보안 중지 -** 재생 창 끝에서 재생을 중지할지 또는 계속할지 여부를 지정할 수 있습니다.
* **RBOP(Resolution Based Output Protection) -** 픽셀 해상도에 따라 출력 제한을 지정할 수 있습니다.
* **CDM 게이팅 -** HTML5를 지원하기 위해 Adobe이 단일 URL 끝점에서 모든 DRM 프로토콜 메시지를 사용할 수 있도록 Adobe Primetime DRM(이전 Adobe 액세스 DRM) Java SDK에 포함된 참조 구현 라이선스 서버를 업데이트했습니다. CDM(Content Decration Module) DRM 공급업체에서 구현해야 하는 HTML5 EMM(Encrypted Media Extension) 사양을 준수하려면 이 HTTP URL 방법을 통합해야 합니다. 이전에는 Reference Implementation 라이선스 서버에서 노출된 유일한 URL 끝점입니다.

   * /flashaccess/i15n/v3(개인화)
   * /flashaccess/license/v5(라이센스 요청)
   * /flashaccess/licenseRet/v5(라이센스 반환)
   * /flashaccess/getServerVersion/v5(서버 버전 가져오기)

이제 모든 요청(HTML5 CDM에서 시작)을 단일 종단점으로 연결할 수 있습니다./req

이 변경 사항은 Flash Player, Android, iOS와 같은 비 CDM 플랫폼과 역호환됩니다.

* **RBOP** 다운스케일링 -HTML5 공간에만 특화된 RBOP에는 자동 다운스케일링 기능이 포함되어 있습니다. 이 경우 DRM 정책에 지정된 허용 비트 전송률을 초과하는 비트 전송률은 허용 가능한 최대 해상도 크기로 축소됩니다. 예를 들어 1080p 스트림이 HDCP 호환 모니터에 컨텐츠를 표시하는 클라이언트로 스트리밍되는 경우 DRM 정책은 최대 해상도가 720p임을 나타낼 수 있습니다. Primetime DRM은 1080p 스트림을 디코딩한 다음 화면에서 렌더링하기 전에 720p로 축소합니다. 비디오를 재생하는 브라우저를 HDCP를 지원하는 모니터로 드래그하면 Primetime DRM이 컨텐츠 다운크기 조정을 중지하고 1080에서 재생할 수 있습니다.

## 버전 5.3 {#known-issues}의 알려진 문제

* `Hasher.bat (flashaccess-hasher.jar)` 출력 로그 메시지 `flashaccess-global.log.`를 Hasher.bat와  `flashaccess-global.log` 파일이 동일한 디렉토리에 있는지 확인해야 합니다.

* 일부 `toJSON()`호출 출력에서는 완전 JSON을 준수하지 않거나 독립형 방법(예: JSON 구조의 구성 없이)으로 완전히 규율되지 않은 `Strings`을 반환합니다.

* Xbox 키 서버는 버전 값이 1이 아닌 키 요청을 수락합니다.

Xbox 키 서버는 버전이 1인 키 요청만 지원하지만 현재 서버에서 버전이 1이 아닌 키 요청을 수락합니다.

* Xbox 키 서버에서 정책의 유효성을 검사하지 않습니다.

Xbox 키 서버는 유효 기간이 지난 정책을 수락하지 않아야 하지만 현재 서버에서 이에 상관없이 수락합니다.

* Xbox 키 서버는 잘못된 패키지 인증서로 생성된 메타데이터가 포함된 키 요청을 거부해야 합니다.
* 일부 JSON 구조의 반환 값이 해상도 기반 출력 보호 관련 클래스에 대해 올바른 형식이 아닙니다.

일부 클래스는 해당 개체의 JSON 호환 표현을 String으로 반환해야 하는 toJSON() 메서드를 구현하지만 현재 반환된 값이 완전히 JSON과 호환되지 않습니다.

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 문서를 참조하십시오.
