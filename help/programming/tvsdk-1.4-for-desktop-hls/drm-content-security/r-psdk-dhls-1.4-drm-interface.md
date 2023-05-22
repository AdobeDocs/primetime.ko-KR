---
description: Primetime DRM(디지털 권한 관리) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.
title: Primetime DRM 인터페이스 개요
exl-id: 8d6b9416-5d8a-4d1e-b8e6-47c43389f079
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Primetime DRM 인터페이스 개요{#primetime-drm-interface-overview}

Primetime DRM(디지털 권한 관리) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM은 TVSDK 애플리케이션에서 콘텐츠 보호를 구현할 수 있는 확장 가능한 효율적인 워크플로를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 만들어 비디오 콘텐츠에 대한 권한을 보호하고 관리합니다.

TVSDK는 Primetime DRM 통합을 사용자 지정 DRM 워크플로우로 지원합니다. 즉, 애플리케이션이 Flash을 사용하여 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다 `DRMManager`. 활성화하려면 `MediaPlayer` 은 인증을 위해 DRM 관리자를 제공합니다.

다음은 DRM 작업을 위한 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어의 참조:

   ```
   public function get drmManager():DRMManager 
   ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

추가적인 관련 API 요소:

* [flash.net.drm.DRMMmanager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

DRM에 대한 자세한 내용은 Adobe Primetime DRM 설명서를 참조하십시오.
