---
description: Adobe Primetime DRM 파섹 Java API 생성을 지원하는 애플리케이션에서 Primetime DRM SDK를 사용하여 DRM 정책을 지정하고 해당 정책을 콘텐츠에 적용하고 해당 컨텐츠를 암호화할 수 있습니다.
seo-description: Adobe Primetime DRM 파섹 Java API 생성을 지원하는 애플리케이션에서 Primetime DRM SDK를 사용하여 DRM 정책을 지정하고 해당 정책을 콘텐츠에 적용하고 해당 컨텐츠를 암호화할 수 있습니다.
seo-title: Adobe Primetime DRM의 새로운 기능
title: Adobe Primetime DRM의 새로운 기능
uuid: 3c8da594-a231-4496-bffc-130775ecae50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Adobe Primetime DRM의 새로운 기능{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM 파섹 Java API 생성을 지원하는 애플리케이션에서 Primetime DRM SDK를 사용하여 DRM 정책을 지정하고 해당 정책을 콘텐츠에 적용하고 해당 컨텐츠를 암호화할 수 있습니다.

>[!NOTE]
>
>Primetime DRM은 이전에 Adobe Access로 불렸으며 그 이전에는 Flash Access였습니다.

다음은 컨텐츠 보호 프로세스에 대한 간략한 설명입니다.

1. DRM Java API를 사용하여 DRM 정책 속성과 암호화 매개 변수를 설정합니다.
1. 모든 컨텐츠의 사용 역할을 설명하는 DRM 정책을 만듭니다.

   원하는 수의 DRM 정책을 만들 수 있습니다. 대부분의 사용자는 적은 수의 정책을 만든 다음 여러 파일에 적용합니다.
1. 미디어 파일을 패키지합니다.

   *`Packaging a file`* 즉, 파일을 암호화한 다음 파일에 DRM 정책을 적용합니다.
1. 사용자에게 라이센스를 발급하려면 라이센스 서버를 구현합니다.

이러한 단계를 완료하면 암호화된 콘텐츠를 배포할 수 있습니다. 배포가 완료되면 클라이언트는 라이센스 서버에서 라이센스를 요청할 수 있으며 수신한 후에는 컨텐츠를 재생할 수 있습니다.

Primetime DRM SDK는 이러한 작업을 완료하는 Java API를 제공합니다. SDK에는 라이센스 서버와 명령줄 도구의 참조 구현이 포함되어 있으며, 두 도구 모두 DRM SDK Java API를 기반으로 합니다.

아래 설명된 기능은 이번 릴리스의 새로운 기능입니다.

## 새로운 기능 {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **하드 정지 - 재생** 창의 끝에서 재생을 중지할지 또는 계속할지를 지정할 수 있습니다.
* **해상도 종속 출력 컨트롤 - 픽셀 해상도를** 기반으로 출력 제한을 지정할 수 있습니다.
* **라이센스 서버 응답 익명화 - Primetime DRM License Server 프로토콜을** 사용하여 개인 정보를 향상시키기 위해 지원 클라이언트에 대한 라이센스 서버 응답에 대해 전송 인증서 일련 번호가 0으로 지정됩니다.

