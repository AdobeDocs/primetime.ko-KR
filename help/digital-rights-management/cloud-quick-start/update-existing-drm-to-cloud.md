---
title: 클라우드 DRM을 사용하도록 기존 DRM 콘텐츠 업데이트(선택 사항)
description: 클라우드 DRM을 사용하도록 기존 DRM 콘텐츠 업데이트(선택 사항)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# 클라우드 DRM을 사용하도록 기존 DRM 콘텐츠 업데이트(선택 사항) {#update-existing-drm-content-to-use-cloud-drm-optional}

Primetime DRM으로 보호되는 기존 콘텐츠 라이브러리가 있는 경우 원본 소스 파일을 다시 패키지하거나 암호화하지 않고도 Primetime Cloud DRM 서비스를 사용하도록 기존 콘텐츠를 &quot;다시 헤더&quot;할 수 있습니다. 콘텐츠를 재정의하면 HLS 매니페스트에 있는 콘텐츠의 DRM 메타데이터가 업데이트됩니다. 원본 에셋의 암호화 해제/다시 암호화를 수행하지 않습니다. 원본 소스 콘텐트를 사용할 수 없거나 대규모 라이브러리를 다시 패키지하는 데 필요한 리소스 양에 대한 우려가 있는 경우 이 옵션이 유용할 수 있습니다.

Primetime DRM Java SDK를 사용하여 프로그래밍 방식으로 메타데이터를 업데이트할 수 있습니다. 또한 이 보호 키트에 포함된 [!DNL OfflinePackager.jar] 명령줄 도구는 `-drm_refresh` 옵션을 사용하여 이 작업을 수행할 수도 있습니다.

## 다시 머리글 세부 사항 {#section_3F3980D8E775450588C64E02A8448189}

CloudDRM을 사용하려면 재헤더링을 업데이트해야 합니다.

* 라이센스 서버 URL(To [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 라이선스 서버 인증서(CloudDRM 라이선스 서버 인증서)
* 전송 인증서(CloudDRM 전송 인증서로)
* Packager 자격 증명(CloudDRM에서 사용하도록 활성화한 패키저 자격 증명)

## DRM 메타데이터 찾기 {#section_28721CB7966F40708AEC8637F2E9BB72}

HDS 또는 HLS와 같은 HTTP 기술을 사용하는 콘텐트는 Adobe 액세스 DRM 메타데이터를 참조하는 매니페스트를 사용합니다. HDS에서 메타데이터는 `<drmmeta>` 태그에서 참조되며 HLS에서는 `#EXT-X-FAXS-CM` 태그에서 참조됩니다. 두 가지 시나리오에서 메타데이터는 매니페스트에 인라인으로 포함되거나 기본 64 인코딩된 BLOB로 포함되거나 외부에서 이진 파일로 참조할 수 있습니다. 메타데이터가 매니페스트에 포함/인라인인 경우 해당 데이터를 사용하여 DRM 메타데이터를 인스턴스화하기 전에 먼저 기본64를 이진 데이터로 디코딩해야 할 수 있습니다.

## 포함된 OfflinePackager.jar {#section_37C2091856E44AA380D742C72B4DD1A7} 사용

명령줄에 `-drm_refresh option`을 입력합니다. 콘텐츠가 다시 암호화되지 않지만 업데이트된 DRM 메타데이터로 새 매니페스트 파일이 만들어집니다.

## Primetime DRM Java SDK를 사용하여 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2} 다시 헤더 사용

프로그래머틱 방식으로 Primetime DRM(이전 Adobe Access DRM) Java SDK를 사용하면 기존 DRM 메타데이터를 업데이트할 수 있습니다. 자세한 내용은 SDK의 [!DNL /Reference Implmentation/Command Line Tools/samples/] 패키지에 있는 [!DNL RegenerateMetadata.java] 코드 샘플을 참조하십시오. Adobe 액세스 Java SDK는 이 CloudDRM 보호 키트의 일부가 아니며 Adobe에서 직접 취득해야 합니다. 자세한 내용은 Adobe 비즈니스 담당자에게 문의하십시오.