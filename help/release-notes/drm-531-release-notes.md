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

---


# DRM 5.3.1 릴리스 노트 {#drm-release-notes}

DRM 5.3.1 릴리스 노트는 DRM 5.3.1의 새로운 기능과 알려진 문제를 설명합니다.

## 버전 5.3의 새로운 기능 {#new-features}

* **보안 중지 - 재생** 창의 끝에서 재생을 중지할지 또는 계속할지를 지정할 수 있습니다.
* **RBOP(Resolution Based Output Protection) -** 픽셀 해상도를 기반으로 출력 제한을 지정할 수 있습니다.
* **CDM 게이팅 - Adobe는 HTML5를 지원하기 위해** Adobe Primetime DRM(이전 Adobe Access DRM) Java SDK에 포함된 참조 구현 라이선스 서버를 업데이트하여 단일 URL 끝점에서 모든 DRM 프로토콜 메시지를 사용할 수 있도록 했습니다. CDM(Content Decryption Module) DRM 벤더가 구현해야 하는 HTML5 EMM(Encrypted Media Extension) 사양을 준수하려면 이 HTTP URL 메서드를 통합해야 합니다. 이전에는 참조 구현 라이선스 서버에서 노출된 유일한 URL 끝점입니다.

   * /flashaccess/i15n/v3(개인화)
   * /flashaccess/license/v5(라이센스 요청)
   * /flashaccess/licenseRet/v5(라이센스 반환)
   * /flashaccess/getServerVersion/v5(서버 버전 가져오기)

이제 모든 요청(HTML5 CDM에서 시작)을 단일 종단점으로 연결할 수 있습니다./req

이 변경 사항은 Flash Player, Android, iOS와 같은 비 CDM 플랫폼과 역호환됩니다.

* **RBOP 다운스케일링 - RBOP에는 HTML5 공간에 따라** RBOP의 자동 다운스케일링 기능이 포함되어 있습니다. 이 기능은 DRM 정책에 지정된 허용 비트 전송률을 초과하는 비트 전송률을 초과하는 경우 허용 가능한 최대 해상도로 축소됩니다. 예를 들어 1080p 스트림이 비 HDCP 호환 모니터에서 컨텐츠를 표시하는 클라이언트로 스트리밍되는 경우 DRM 정책은 최대 해상도가 720p임을 나타낼 수 있습니다. Primetime DRM은 1080p 스트림을 디코딩한 다음 스크린으로 렌더링하기 전에 720p로 축소합니다. 비디오를 재생하는 브라우저를 HDCP를 지원하는 모니터로 드래그하면 Primetime DRM이 컨텐츠 다운스케일을 중단하고 1080에 재생할 수 있습니다.

## 버전 5.3의 알려진 문제 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` 출력 로그 메시지를 `flashaccess-global.log.`Hasher.bat와 `flashaccess-global.log` 파일이 동일한 디렉토리에 있는지 확인해야 합니다.

* JSON을 완전히 준수하지 않거나 독립형 방식으로 완전히 규율되지 않는 일부 `toJSON()`호출 `Strings` 결과물(예: JSON 구조의 구성 없음)

* Xbox 키 서버는 버전 값이 1이 아닌 키 요청을 수락합니다.

Xbox 키 서버는 버전이 1인 키 요청만 지원하지만 현재 서버가 버전이 1이 아닌 키 요청을 수락합니다.

* Xbox 키 서버에서 정책의 유효성을 제대로 확인하지 않습니다.

Xbox 키 서버는 유효 기간이 지난 정책을 수락하지 말아야 하지만 현재 서버에서 이에 상관없이 수락합니다.

* Xbox 키 서버는 잘못된 패키저 인증서로 생성된 메타데이터가 포함된 키 요청을 거부해야 합니다.
* 일부 JSON 구조의 반환 값이 해상도 기반 출력 보호 관련 클래스에 대해 올바른 형식이 아닙니다.

일부 클래스는 해당 개체의 JSON 호환 표현을 String으로 반환해야 하는 toJSON() 메서드를 구현하지만 현재 반환되는 값은 JSON과 완전히 호환되지 않습니다.

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.
