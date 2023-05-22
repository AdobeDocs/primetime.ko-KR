---
title: DRM 5.3.1 릴리스 노트
description: DRM 5.3.1 릴리스 노트 에서는 DRM 5.3.1의 새로운 기능과 알려진 문제를 설명합니다.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: e4e0a933-cfc6-4713-ae13-5df11cfc1aad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# DRM 5.3.1 릴리스 노트 {#drm-release-notes}

DRM 5.3.1 릴리스 노트 에서는 DRM 5.3.1의 새로운 기능과 알려진 문제를 설명합니다.

## 버전 5.3의 새로운 기능 {#new-features}

* **보안 중지 -** 재생 창 끝에서 재생을 중지할지 또는 계속할지 여부를 지정할 수 있습니다.
* **해상도 기반 출력 보호(RBOP) -** 픽셀 해상도에 따라 출력 구속을 지정할 수 있습니다.
* **CDM 게이트 -** HTML5를 지원하기 위해 Adobe은 Adobe Primetime DRM(이전의 Adobe 액세스 DRM) Java SDK에 포함된 참조 구현 라이선스 서버를 업데이트하여 단일 URL 끝점에서 모든 DRM 프로토콜 메시지를 사용할 수 있습니다. CDM(Content Decryption Module) DRM 공급업체에 의해 구현되어야 하는 HTML5 EME(Encrypted Media Extension) 사양을 준수하려면 HTTP URL 메서드를 통합해야 합니다. 이전에는 참조 구현 라이선스 서버에 의해 노출된 유일한 URL 끝점입니다.

   * /flashaccess/i15n/v3(개별화)
   * /flashaccess/license/v5(라이센스 요청)
   * /flashaccess/licenseRet/v5(라이센스 반환)
   * /flashaccess/getServerVersion/v5(서버 버전 가져오기)

이제 모든 요청(HTML 5 CDM에서 시작)을 단일 끝점으로 보낼 수 있습니다. /req

이 변경 사항은 Flash Player, Android, iOS과 같은 비 CDM 플랫폼과 역호환됩니다.

* **RBOP 하향 조정 -** HTML5 공간에 따라 RBOP에는 자동 다운스케일링 기능이 포함됩니다. 여기서 DRM 정책에 지정된 허용 비트율을 초과하는 비트율이 사용되면 콘텐츠는 최대 허용 해상도로 다운스케일링됩니다. 예를 들어, 1080p 스트림이 비-HDCP 준수 모니터에 콘텐츠를 디스플레이하고 있는 클라이언트로 스트리밍되는 경우, DRM 정책은 최대 해상도가 720p이어야 함을 나타낼 수 있다. Primetime DRM은 1080p 스트림을 디코딩한 다음 화면에 렌더링하기 전에 720p로 다운스케일링합니다. 그런 다음 비디오를 재생하는 브라우저가 HDCP를 지원하는 모니터로 드래그되면 Primetime DRM은 컨텐츠의 다운스케일링을 중단하고 1080에서 다시 재생할 수 있도록 합니다.

## 버전 5.3의 알려진 문제 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` 로그 메시지를 다음으로 출력 `flashaccess-global.log.`다음을 확인해야 합니다. `flashaccess-global.log` 파일이 Hasher.bat와 동일한 디렉터리에 있습니다.

* 일부 의 출력 `toJSON()`호출 반환 `Strings` 독립 실행형 방식(즉, JSON 구조의 구성 없이)으로 완전히 JSON 호환 또는 완전히 호환되지 않는 경우입니다.

* Xbox 키 서버는 버전 값이 1이 아닌 키 요청을 수락합니다.

Xbox 키 서버는 버전이 1과 동일한 키 요청만 지원해야 하지만 현재 서버는 버전이 1이 아닌 키 요청을 수락합니다.

* Xbox 키 서버가 정책을 올바르게 확인하지 않습니다.

Xbox 키 서버는 유효 날짜 이후의 정책을 수락하지 않아야 하지만 현재 서버는 해당 정책에 관계없이 수락합니다.

* Xbox 키 서버는 잘못된 패키지 인증서로 생성된 메타데이터가 포함된 키 요청을 거부해야 합니다.
* 일부 JSON 구조의 반환된 값의 형식이 해상도 기반 출력 보호 관련 클래스에 대해 올바르게 지정되지 않았습니다.

일부 클래스는 해당 객체의 JSON 호환 표현을 문자열로 반환해야 하는 toJSON() 메서드를 구현하지만 현재 반환된 값이 완전히 JSON 규격이 아닙니다.

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
