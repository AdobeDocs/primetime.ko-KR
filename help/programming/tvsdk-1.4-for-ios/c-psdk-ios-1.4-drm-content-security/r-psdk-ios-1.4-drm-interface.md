---
description: Primetime DRM(디지털 권한 관리) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.
title: Primetime DRM 인터페이스 개요
exl-id: dee420cf-8aad-42e8-965d-9fd9395f2c45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Primetime DRM 인터페이스 개요 {#primetime-drm-interface-overview}

Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 Adobe의 통합 Primetime DRM 솔루션 대신 타사 DRM 솔루션을 사용할 수 있습니다.

타사 DRM 솔루션의 가용성에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

Primetime DRM(디지털 권한 관리) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM은 TVSDK 애플리케이션에서 콘텐츠 보호를 구현할 수 있는 확장 가능한 효율적인 워크플로를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 만들어 비디오 콘텐츠에 대한 권한을 보호하고 관리합니다.

TVSDK는 Primetime DRM 통합을 사용자 지정 DRM 워크플로우로 지원합니다. 즉, 애플리케이션이 Flash DRMManager를 사용하여 스트림을 재생하기 전에 DRM 인증 워크플로우를 구현해야 합니다. 이를 활성화하기 위해 MediaPlayer는 인증을 위한 DRM 관리자를 제공합니다.

TVSDK 패키지에 포함된 DRM 샘플 플레이어 코드를 참조하십시오.

다음은 DRM 작업을 위한 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어의 참조:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK 문제 a `PTMediaPlayerItemDRMMetadataChanged` drm 메타데이터가 변경될 때 알립니다. 이 메타데이터는 의 거의 모든 함수에 대한 입력으로 사용됩니다. `DRMManager` 클래스.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

DRM 보호 스트림이 MBR(Multiple Bit-rate) 인코딩되는 경우, 변형 플레이리스트에 사용되는 DRM 메타데이터는 모든 비트 레이트 스트림에서 사용되는 메타데이터와 동일해야 한다.

>[!TIP]
>
>iOS 앱에서 DRM 보호 에셋 URL을 참조할 때 쿼리 문자열 매개 변수 `?faxs=1` 은(는) (MBR) 집합 수준 M3U8 URL에 추가되어야 합니다. 예:
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>다음 `faxs=1` 쿼리 문자열 매개 변수는 콘텐츠가 DRM으로 보호됨을 알리고, iOS TVSDK에서 그에 따라 DRM 해독 워크플로우를 트리거합니다. 다음을 추가할 수도 있습니다 `faxs=1` 다른 플랫폼으로 지정된 DRM 보호 HLS 에셋 URL의 태그입니다. iOS에서 필요한 것으로 관찰되거나 다른 플랫폼의 플레이어에서 non-op로 처리됩니다.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

DRM에 대한 자세한 내용은 [Adobe Primetime DRM 설명서](https://help.adobe.com/en_US/primetime/drm).

## TSDK 응용 프로그램에서 Primetime DRM 구현 {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM은 TVSDK에 통합되어 있으므로 TVSDK 애플리케이션에서 콘텐츠 보호를 간편하게 구현할 수 있습니다.

Primetime DRM을 사용하여 TVSDK 애플리케이션에서 콘텐츠 보호를 구현하는 방법에 대한 개요 및 자세한 내용은 다음을 참조하십시오.

* [Adobe Primetime TVSDK-DRM 워크플로(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
