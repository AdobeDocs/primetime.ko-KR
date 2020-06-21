---
description: 'Adobe® Access™는 고부가가치 시청각 컨텐츠를 위한 고급 디지털 권한 관리 및 컨텐츠 보호 솔루션입니다. Java API를 사용하여 만드는 도구를 사용하여 정책을 만들고 오디오 및 비디오 컨텐츠가 포함된 파일에 정책을 적용하고 이러한 파일을 암호화할 수 있습니다. 이러한 작업을 수행하기 위한 고급 단계는 다음과 같습니다. '
seo-description: 'Adobe® Access™는 고부가가치 시청각 컨텐츠를 위한 고급 디지털 권한 관리 및 컨텐츠 보호 솔루션입니다. Java API를 사용하여 만드는 도구를 사용하여 정책을 만들고 오디오 및 비디오 컨텐츠가 포함된 파일에 정책을 적용하고 이러한 파일을 암호화할 수 있습니다. 이러한 작업을 수행하기 위한 고급 단계는 다음과 같습니다. '
seo-title: 개요
title: 개요
uuid: 874c175b-8207-49fa-aad4-204ccbee9c2c
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# 개요 {#overview}

Adobe® Access™는 고부가가치 시청각 컨텐츠를 위한 고급 디지털 권한 관리 및 컨텐츠 보호 솔루션입니다. Java API를 사용하여 만드는 도구를 사용하여 정책을 만들고 오디오 및 비디오 컨텐츠가 포함된 파일에 정책을 적용하고 이러한 파일을 암호화할 수 있습니다. 이러한 작업을 수행하기 위한 고급 단계는 다음과 같습니다.

1. Java API를 사용하여 정책 속성 및 암호화 매개 변수를 설정합니다.
1. 컨텐츠의 사용 역할을 설명하는 정책을 만듭니다. (정책 [작업](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)참조).

   원하는 수의 정책을 만들 수 있습니다. 대부분의 사용자는 적은 수의 정책을 만들어 여러 파일에 적용합니다.

1. 미디어 파일을 패키지합니다.

   따라서 파일 *을* 패키징하는 것은 파일을 암호화하여 정책을 적용하는 것을 의미합니다. (미디어 파일 [패키징을 참조하십시오](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. 사용자에게 라이선스를 발급하려면 라이선스 서버를 구현합니다.

이제 암호화된 콘텐츠를 배포할 수 있으며 클라이언트는 서버에서 라이센스를 요청할 수 있습니다.

SDK는 이러한 작업을 수행하는 Java API를 제공하며, 라이센스 서버의 참조 구현 및 Java API를 기반으로 하는 명령줄 도구를 포함합니다. 자세한 내용은 Adobe *Access 참조 구현 사용을 참조하십시오*.

## Adobe Access 5.2의 새로운 기능 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **외부 CEK**: CEK를 암호화하고 이를 컨텐츠 메타데이터에 번들로 제공하는 대신 CKMS(Content Key Management System)를 DRM 라이선스 서비스 및 컨텐츠 패키징 워크플로우에 통합할 수 있습니다. Adobe [Access DRM 외부 CEK 개요를 참조하십시오](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **라이선스(바우처) 반환**: 클라이언트가 클라이언트에 발급된 라이센스를 반환(또는 삭제)하는 기능
* **Xbox 키 서버**: Xbox 및 Xbox 360으로 보낸 콘텐츠를 보호할 수 있습니다. (Adobe Primetime 클라이언트는 필수)

## 사용자 지정 사용 규칙 {#custom-usage-rules}

사용자 지정 사용 규칙을 지정합니다. 사용자 지정 데이터는 라이센스 서버에서 발행한 라이센스에 포함될 수 있습니다. 이 데이터의 해석/처리는 클라이언트 응용 프로그램 및 라이센스 서버의 구현에 전적으로 달려 있습니다.

사용 사례 예: 정책 및/또는 컨텐츠 라이선스의 일부로 다른 비즈니스 규칙을 안전하게 전달하여 사용 규칙을 확장할 수 있습니다. 보안상의 이유로 이러한 사용 규칙은 사용자 정의 클라이언트 응용 프로그램 코드에 적용되기 때문에 이 옵션을 AIR 응용 프로그램 또는 Flash Player SWF 허용 목록 옵션과 함께 사용해야 합니다. 자세한 내용은 &quot;[런타임 및 애플리케이션 제한](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md)사항&quot;을 참조하십시오.
