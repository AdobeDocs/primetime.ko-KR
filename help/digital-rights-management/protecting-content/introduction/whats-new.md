---
description: Adobe Primetime DRM은 고부가가치 시청각 콘텐츠를 위한 고급 Digital Rights Management(DRM) 및 콘텐츠 보호 솔루션입니다. Java API 생성을 지원하는 애플리케이션에서 Primetime DRM SDK를 사용하여 DRM 정책을 지정하고, 이러한 정책을 콘텐츠에 적용하고, 해당 콘텐츠를 암호화할 수 있습니다.
title: Adobe Primetime DRM의 새로운 기능
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Adobe Primetime DRM의 새로운 기능{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM은 고부가가치 시청각 콘텐츠를 위한 고급 Digital Rights Management(DRM) 및 콘텐츠 보호 솔루션입니다. Java API 생성을 지원하는 애플리케이션에서 Primetime DRM SDK를 사용하여 DRM 정책을 지정하고, 이러한 정책을 콘텐츠에 적용하고, 해당 콘텐츠를 암호화할 수 있습니다.

>[!NOTE]
>
>Primetime DRM은 이전에 Adobe 액세스라고 하였으며, 그 이전에는 Flash Access라고 했습니다.

다음은 콘텐츠 보호 프로세스에 대한 대략적인 설명입니다.

1. DRM Java API를 사용하여 DRM 정책 속성 및 암호화 매개변수를 설정합니다.
1. 콘텐츠에 대한 사용 역할을 설명하는 DRM 정책을 만듭니다.

   원하는 수만큼 DRM 정책을 생성할 수 있습니다. 대부분의 사용자는 적은 수의 정책을 만든 다음 많은 파일에 적용합니다.
1. 미디어 파일을 패키징합니다.

   *`Packaging a file`* 는 파일을 암호화한 다음 DRM 정책을 파일에 적용함을 의미합니다.
1. 라이선스 서버를 구현하여 사용자에게 라이선스를 발급합니다.

이 단계를 완료하면 암호화된 콘텐츠를 배포할 준비가 된 것입니다. 배포 후 클라이언트는 라이센스 서버에 라이센스를 요청할 수 있으며 수신시 콘텐츠를 재생할 수 있습니다.

Primetime DRM SDK는 이러한 작업을 완료하기 위한 Java API를 제공합니다. SDK에는 라이센스 서버와 명령줄 도구의 참조 구현이 포함되어 있으며, 둘 다 DRM SDK Java API를 기반으로 합니다.

아래에 설명된 기능은 이 릴리스의 새로운 기능입니다.

## 새로운 기능 {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **하드 스톱 -** 재생 창 끝에서 재생을 중지할지 또는 계속할지 여부를 지정할 수 있습니다.
* **해상도 종속 출력 제어 -** 픽셀 해상도에 따라 출력 구속을 지정할 수 있습니다.
* **라이선스 서버 응답 익명화 -** Primetime DRM 라이선스 서버 프로토콜을 사용하여 개인 정보를 강화하기 위해 전송 인증서 일련 번호는 지원 클라이언트에 대한 라이선스 서버 응답에 대해 0으로 설정됩니다.
