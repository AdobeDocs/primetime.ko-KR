---
description: Adobe® 액세스™은 고부가가치 시청각 콘텐츠를 위한 고급 디지털 권한 관리 및 콘텐츠 보호 솔루션입니다. Java API를 사용하여 만드는 도구를 사용하여 정책을 만들고, 오디오 및 비디오 콘텐츠가 들어 있는 파일에 정책을 적용하고, 해당 파일을 암호화할 수 있습니다. 이러한 작업을 수행하기 위한 높은 수준의 단계는 다음과 같다
title: 개요
exl-id: cf081058-9b41-4b09-9258-a7d873799846
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 개요 {#overview}

Adobe® 액세스™은 고부가가치 시청각 콘텐츠를 위한 고급 디지털 권한 관리 및 콘텐츠 보호 솔루션입니다. Java API를 사용하여 만드는 도구를 사용하여 정책을 만들고, 오디오 및 비디오 콘텐츠가 들어 있는 파일에 정책을 적용하고, 해당 파일을 암호화할 수 있습니다. 이러한 작업을 수행하기 위한 높은 수준의 단계는 다음과 같습니다.

1. Java API를 사용하여 정책 속성 및 암호화 매개 변수를 설정합니다.
1. 콘텐츠의 사용 역할을 설명하는 정책을 만듭니다. (참조: [정책 작업](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   원하는 수만큼 정책을 생성할 수 있습니다. 대부분의 사용자는 적은 수의 정책을 만들어 많은 파일에 적용합니다.

1. 미디어 파일을 패키징합니다.

   이 맥락에서, *파일 패키징* 는 변수를 암호화하고 정책을 적용하는 것을 의미합니다. (참조: [미디어 파일 패키징](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. 라이선스 서버를 구현하여 사용자에게 라이선스를 발급합니다.

이제 암호화된 콘텐츠를 배포할 준비가 되었으며 클라이언트는 서버에 라이선스를 요청할 수 있습니다.

SDK는 이러한 작업을 수행하기 위한 Java API를 제공하며 라이선스 서버의 참조 구현 및 Java API를 기반으로 하는 명령줄 도구를 포함합니다. 자세한 내용은 *Adobe 액세스 참조 구현 사용*.

## Adobe 액세스 5.2의 새로운 기능 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **외부 확인**: CEK를 암호화하고 콘텐츠의 메타데이터에 번들로 변환하는 대신 DRM 라이센스 서비스 및 콘텐츠 패키징 워크플로우에 CKMS(콘텐츠 키 관리 시스템)를 통합하는 기능. 다음을 참조하십시오 [Adobe 액세스 DRM 외부 CEK 개요](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **라이선스(바우처) 반환**: 클라이언트가 클라이언트에 발급된 라이선스를 반환(또는 삭제)하는 기능입니다.
* **Xbox 키 서버**: Xbox 및 Xbox 360으로 전송되는 콘텐츠를 보호하는 기능. (Adobe Primetime 클라이언트가 필요합니다.)

## 사용자 정의 사용 규칙 {#custom-usage-rules}

사용자 지정 사용 규칙을 지정합니다. 사용자 지정 데이터는 라이선스 서버에서 발급한 라이선스에 포함될 수 있습니다. 이 데이터의 해석/처리는 전적으로 클라이언트 애플리케이션 및 라이센스 서버의 구현에 따라 결정됩니다.

예제 사용 사례: 다른 비즈니스 규칙이 정책 및/또는 콘텐츠 라이선스의 일부로 안전하게 전달될 수 있도록 하여 사용 규칙의 확장성을 활성화합니다. 보안상의 이유로 이러한 사용 규칙은 사용자 정의 클라이언트 애플리케이션 코드에 적용되므로 이 옵션은 AIR 애플리케이션 또는 Flash Player SWF 허용 목록 옵션과 함께 사용해야 합니다. 자세한 내용은 [런타임 및 애플리케이션 제한 사항](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
