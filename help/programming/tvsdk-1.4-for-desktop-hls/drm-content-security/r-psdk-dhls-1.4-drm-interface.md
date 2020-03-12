---
description: Primetime 디지털 저작권 관리(DRM 파섹) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.
seo-description: Primetime 디지털 저작권 관리(DRM 파섹) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.
seo-title: Primetime DRM 인터페이스 개요
title: Primetime DRM 인터페이스 개요
uuid: 01714ee6-a937-4ca3-b535-6a6ef681ee6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Primetime DRM 인터페이스 개요{#primetime-drm-interface-overview}

Primetime 디지털 저작권 관리(DRM 파섹) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM은 TVSDK 애플리케이션에서 컨텐츠 보호를 구현하는 확장 가능하고 효율적인 워크플로우를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 만들어 비디오 컨텐츠에 대한 권한을 보호하고 관리할 수 있습니다.

TVSDK는 Primetime DRM 통합을 맞춤형 DRM 워크플로우로 지원합니다. 즉, Flash를 사용하여 스트림을 재생하기 전에 응용 프로그램이 DRM 인증 워크플로우를 구현해야 합니다 `DRMManager`. 이를 활성화하려면 인증을 위한 DRM 관리자를 `MediaPlayer` 제공합니다.

다음은 DRM을 사용하여 작업하는 데 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어의 참조입니다.

   ```
   public function get drmManager():DRMManager 
   ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

추가 관련 API 요소:

* [flash.net.drm.DRMManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

DRM에 대한 자세한 내용은 Adobe Primetime DRM 설명서를 참조하십시오.
