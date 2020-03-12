---
description: Adobe의 Primetime Access DRM 솔루션에 익숙한 사용자에게는 Access와 ExpressPlay 솔루션을 기반으로 하는 Primetime Cloud DRM이 기본적으로 서로 다릅니다.
seo-description: Adobe의 Primetime Access DRM 솔루션에 익숙한 사용자에게는 Access와 ExpressPlay 솔루션을 기반으로 하는 Primetime Cloud DRM이 기본적으로 서로 다릅니다.
seo-title: Access에서 다중 DRM으로 마이그레이션
title: Access에서 다중 DRM으로 마이그레이션
uuid: 3e33ca9a-867e-46b8-bf88-8dbfe14ff786
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Access에서 다중 DRM으로 마이그레이션 {#migrating-from-access-to-multi-drm}

Adobe의 Primetime Access DRM 솔루션에 익숙한 사용자에게는 Access와 ExpressPlay 솔루션을 기반으로 하는 Primetime Cloud DRM이 기본적으로 서로 다릅니다.

## 접근과 DRM의 건축적 차이점

|  | 액세스 | 다중 DRM |
|---|---|---|
| **패키징** | Packager는 라이센스 서버에 바인딩되어 있습니다. 콘텐트를 패키지화할 때 Packager는 라이센스 서버의 공개 키를 알고 있어야 합니다. | Packager가 하나의 라이센스 서버에 바인딩되어 있지 않습니다. |
|  | 컨텐츠가 패키지되면 특정 라이센스 서버에 바인딩됩니다. | 컨텐츠가 특정 라이센스 서버에 바인딩되어 있지 않습니다. 이러한 효과의 한 가지 이점은 프로덕션 라이선스를 받기 전에 모든 컨텐츠를 패키지화할 수 있다는 것입니다. |
|  | 키는 암호화된 후 컨텐츠 자체(메타데이터에 포함)에 안전하게 포함되므로 Packager는 어떠한 형태의 키 저장소와 통신할 필요가 없습니다. 해당 라이센스 서버만 읽을 수 있습니다. | 키 *스토리지 시스템에서* 패키저로 *전송하거나 Packager* 에서주요 스토리지 시스템으로 보내야 합니다. 핵심 스토리지 시스템은 고객의 자체 시스템이거나 ExpressPlay의 키 스토리지가 될 수 있습니다. |
| **권한 부여** | 클라이언트가 Access Cloud 서비스에 콘텐츠를 요청합니다. 그러면 Access 클라우드 서비스가 고객의 권한 부여 시스템에 요청을 합니다. 고객의 권한 부여 시스템은 고객의 권한 부여와 다시 응답합니다. (클라이언트는 라이센스 요청을 하기 전에 고객의 서버에서 로그인하기 위한 쿠키를 받았을 수 있습니다.) | 클라이언트는 고객의 스토어프런트에서 토큰을 요청합니다(이는 고객이 이전에 인증 쿠키를 받았던 워크플로우와 동일할 수 있습니다). 현재 고객은 권한 확인을 수행합니다. 권한 확인이 전달되면 고객은 ExpressPlay 서버에 요청을 보내 고객을 위한 토큰을 생성합니다. 이 토큰은 항상 특정 콘텐츠에 바인딩되며 특정 장치에 바인딩될 *수* 있습니다. 고객의 스토어 홈페이지에서 토큰을 다시 클라이언트로 보냅니다. 클라이언트가 DRM 재생 요청을 하면 토큰은 요청에 포함되고(장치 관련 방법) ExpressPlay의 DRM 서버는 고객의 서버에 호출하지 않고 토큰의 유효성을 검사합니다. |