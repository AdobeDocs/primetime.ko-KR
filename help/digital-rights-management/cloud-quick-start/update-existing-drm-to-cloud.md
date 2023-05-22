---
title: 클라우드 DRM을 사용하도록 기존 DRM 콘텐츠 업데이트(선택 사항)
description: 클라우드 DRM을 사용하도록 기존 DRM 콘텐츠 업데이트(선택 사항)
copied-description: true
exl-id: 89b1e99a-cb28-4524-9c47-f71f92d3753d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 클라우드 DRM을 사용하도록 기존 DRM 콘텐츠 업데이트(선택 사항) {#update-existing-drm-content-to-use-cloud-drm-optional}

Primetime DRM으로 보호되는 기존 콘텐츠 라이브러리가 있는 경우 원본 소스 파일을 다시 패키지/암호화하는 대신 Primetime Cloud DRM 서비스를 사용하도록 기존 콘텐츠를 &quot;다시 헤더&quot;할 수 있습니다. 콘텐츠를 다시 헤더하면 HLS 매니페스트에서 콘텐츠의 DRM 메타데이터만 업데이트됩니다. 원본 자산의 암호화 해제/재암호화를 수행하지 않습니다. 원본 소스 콘텐츠를 사용할 수 없거나 큰 라이브러리를 다시 패키지하는 데 필요한 리소스의 양이 걱정되는 경우 이 방법이 유용한 옵션이 될 수 있습니다.

Primetime DRM Java SDK를 사용하여 메타데이터를 프로그래밍 방식으로 업데이트할 수 있습니다. 또한 [!DNL OfflinePackager.jar] 이 보호 키트에 포함된 명령줄 도구는 `-drm_refresh` 옵션을 선택합니다.

## 세부 정보 헤더 다시 지정 {#section_3F3980D8E775450588C64E02A8448189}

CloudDRM을 사용하려면 재머리글이 다음 필드를 업데이트해야 합니다.

* 라이선스 서버 URL(대상 [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* 라이선스 서버 인증서(CloudDRM 라이선스 서버 인증서에 대한)
* 전송 인증서(CloudDRM 전송 인증서로)
* 패키지 자격 증명(CloudDRM에 사용하기 위해 활성화한 패키지 자격 증명에)

## DRM 메타데이터 찾기 {#section_28721CB7966F40708AEC8637F2E9BB72}

HTTP 기술(예: HDS 또는 HLS)을 사용하는 콘텐츠는 Adobe 액세스 DRM 메타데이터를 참조하는 매니페스트를 사용합니다. HDS에서 메타데이터는 `<drmmeta>` 태그 및 HLS에서는 `#EXT-X-FAXS-CM` 태그에 가깝게 배치하십시오. 두 시나리오 중 하나에서 메타데이터는 매니페스트에 base-64 인코딩 blob로 인라인으로 포함되거나 외부에서 이진 파일로 참조될 수 있습니다. 메타데이터가 매니페스트에 임베드되거나 인라인된 경우 해당 데이터를 사용하여 DRM 메타데이터를 인스턴스화하기 전에 먼저 base64에서 메타데이터를 이진 데이터로 디코딩해야 할 수 있습니다.

## 포함된 OfflinePackage.jar 사용 {#section_37C2091856E44AA380D742C72B4DD1A7}

를 제공합니다. `-drm_refresh option` 명령줄에 연결합니다. 콘텐츠가 다시 암호화되지 않지만 새 매니페스트 파일은 업데이트된 DRM 메타데이터로 만들어집니다.

## Primetime DRM Java SDK를 사용하여 다시 헤더 {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

기존 DRM 메타데이터를 업데이트하려면 프로그래밍 방식으로 Primetime DRM(이전의 Adobe 액세스 DRM) Java SDK를 사용하여 수행할 수 있습니다. 자세한 내용은 다음을 참조하십시오 [!DNL RegenerateMetadata.java] 의 코드 샘플 [!DNL /Reference Implmentation/Command Line Tools/samples/] SDK 패키지. Adobe 액세스 Java SDK는 이 CloudDRM 보호 키트의 일부가 아니므로 Adobe에서 직접 획득해야 합니다. 자세한 내용은 Adobe 비즈니스 담당자에게 문의하십시오.
