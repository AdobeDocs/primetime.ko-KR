---
description: Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 제3자 DRM 솔루션을 Adobe의 통합 Primetime DRM 솔루션의 대안으로 사용할 수 있습니다.
keywords: DRM;대시;HLS
title: Primetime DRM 인터페이스 개요
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Primetime DRM 인터페이스 개요 {#primetime-drm-interface-overview}

Primetime Digital Rights Management(DRM) 시스템의 기능을 사용하여 비디오 콘텐츠에 안전하게 액세스할 수 있습니다. 또는 제3자 DRM 솔루션을 Adobe의 통합 Primetime DRM 솔루션의 대안으로 사용할 수 있습니다.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

제3자 DRM 솔루션의 사용 가능성에 대한 최신 정보는 Adobe 담당자에게 문의하십시오.

Primetime 디지털 저작권 관리(DRM) 시스템의 주요 클라이언트측 요소는 DRM 관리자입니다.

Primetime DRM은 TVSDK 애플리케이션에서 컨텐츠 보호를 구현하는 확장 가능하고 효율적인 워크플로우를 제공합니다. 각 디지털 미디어 파일에 대한 라이선스를 생성하여 비디오 컨텐츠에 대한 권한을 보호하고 관리할 수 있습니다.

TVSDK는 Primetime DRM 통합을 맞춤형 DRM 워크플로우로 지원합니다. 즉, Flash DRMManager를 사용하여 스트림을 재생하기 전에 응용 프로그램이 DRM 인증 워크플로우를 구현해야 합니다. 이를 활성화하려면 MediaPlayer에서 인증을 위한 DRM 관리자를 제공합니다.

TVSDK 패키지에 포함된 DRM 샘플 플레이어 코드를 참조하십시오.

다음은 DRM에서 작업하는 데 가장 중요한 API 요소입니다.

* DRM 하위 시스템을 구현하는 DRM 관리자 개체에 대한 미디어 플레이어 참조:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

DRM 메타데이터가 변경되면 TVSDK에서 `PTMediaPlayerItemDRMMetadataChanged` 알림을 발행합니다. 이 메타데이터는 `DRMManager` 클래스의 거의 모든 함수에 대한 입력으로 사용됩니다.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

DRM으로 보호된 스트림이 여러 비트 전송률(MBR)로 인코딩된 경우 변형 재생 목록에 사용되는 DRM 메타데이터는 모든 비트율 스트림에 사용되는 메타데이터와 동일해야 합니다.

>[!TIP]
>
>iOS 앱에서 DRM으로 보호된 자산 URL을 참조하는 경우 쿼리 문자열 매개 변수 `?faxs=1`이(가) 설정된 수준 M3U8 URL에 추가되어야 합니다. 예:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

`faxs=1` 쿼리 문자열 매개 변수는 컨텐츠가 DRM으로 보호되었다는 신호를 주고 iOS TVSDK에서 그에 따라 DRM 암호 해독 워크플로우를 트리거합니다. 다른 플랫폼용으로 지정되는 DRM으로 보호된 HLS 자산 URL에 `faxs=1` 태그를 추가할 수도 있습니다.iOS에서는 필요에 따라 처리되거나 다른 플랫폼의 플레이어에서 비상업자로 취급됩니다.

## TSVDK 응용 프로그램 {#implement-primetime-drm-in-a-tsvdk-application}에서 Primetime DRM 구현

Primetime DRM은 TVSDK에 통합되어 있으므로 TVSDK 애플리케이션에서 컨텐츠 보호 구현을 간소화할 수 있습니다.

Primetime DRM을 사용하여 TVSDK 애플리케이션에서 컨텐츠 보호 구현에 대한 개요와 자세한 내용은 다음을 참조하십시오.

* [Adobe Primetime TVSDK-DRM 워크플로우(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)