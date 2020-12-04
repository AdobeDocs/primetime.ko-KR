---
seo-title: 클라우드 DRM을 사용하도록 기존 DRM 컨텐츠 업데이트(선택 사항)
title: 클라우드 DRM을 사용하도록 기존 DRM 컨텐츠 업데이트(선택 사항)
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# 기존 DRM 콘텐츠를 업데이트하여 클라우드 DRM(선택 사항) {#update-existing-drm-content-to-use-cloud-drm-optional}

Primetime DRM으로 보호되는 기존 콘텐츠 라이브러리가 있는 경우 원본 소스 파일을 다시 패키지하거나 암호화하지 않고도 Primetime Cloud DRM 서비스를 사용하도록 기존 콘텐츠를 &quot;다시 헤더&quot;할 수 있습니다. 콘텐츠를 다시 정의하면 HLS 매니페스트에 있는 콘텐츠의 DRM 메타데이터가 업데이트됩니다. 원본 자산의 암호화 해제/재암호화를 수행하지 않습니다. 원본 소스 콘텐트를 사용할 수 없거나 대규모 라이브러리를 다시 패키지하는 데 필요한 리소스의 양이 우려될 경우 이 옵션이 유용합니다.

Primetime DRM Java SDK를 사용하여 메타데이터를 프로그래밍 방식으로 업데이트할 수 있습니다. 또한 이 보호 키트에 포함된 [!DNL OfflinePackager.jar] 명령줄 도구는 `-drm_refresh` 옵션을 사용하여 이 작업을 수행할 수도 있습니다.

## 재헤더 세부 사항 {#section_3F3980D8E775450588C64E02A8448189}

CloudDRM을 사용하려면 재헤딩(re-header)이 다음 필드를 업데이트해야 합니다.

* 라이센스 서버 URL(tps://access.adobeprimetime.com/flashaccessserver/axs_prod[!DNL ht<span></span>까지)]
* 라이선스 서버 인증서(CloudDRM 라이선스 서버 인증서)
* 전송 인증서(CloudDRM 전송 인증서로)
* Packager 자격 증명(CloudDRM에서 사용하기 위해 활성화한 패키지 자격 증명)

## DRM 메타데이터 찾기 {#section_28721CB7966F40708AEC8637F2E9BB72}

HTTP 기술(예: HDS 또는 HLS)을 사용하는 콘텐트는 Adobe 액세스 DRM 메타데이터를 참조하는 매니페스트를 사용합니다. HDS에서 메타데이터는 `<drmmeta>` 태그에서 참조되며 HLS에서는 `#EXT-X-FAXS-CM` 태그에서 참조됩니다. 두 가지 시나리오에서 메타데이터는 매니페스트에 기본 64 인코딩 blob로 포함되거나, 외부에서 이진 파일로 참조될 수 있습니다. 메타데이터가 매니페스트에 포함/인라인인 경우 해당 데이터를 사용하여 DRM 메타데이터를 인스턴스화하기 전에 먼저 base64를 이진 데이터로 디코딩해야 할 수 있습니다.

## 포함된 OfflinePackager.jar {#section_37C2091856E44AA380D742C72B4DD1A7} 사용

명령줄에 `-drm_refresh option`을 입력합니다. 업데이트된 DRM 메타데이터로 새 매니페스트 파일이 만들어지고 컨텐츠는 다시 암호화되지 않습니다.

## Primetime DRM Java SDK를 사용하여 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2} 재헤더 사용

프로그래머틱 방식으로 Primetime DRM(이전 Adobe Access DRM) Java SDK를 사용하면 기존 DRM 메타데이터를 업데이트할 수 있습니다. 자세한 내용은 SDK의 [!DNL /Reference Implmentation/Command Line Tools/samples/] 패키지에 있는 [!DNL RegenerateMetadata.java] 코드 샘플을 참조하십시오. Adobe 액세스 Java SDK는 이 CloudDRM 보호 키트의 일부가 아니며 Adobe에서 직접 취득해야 합니다. 자세한 내용은 Adobe 비즈니스 담당자에게 문의하십시오.