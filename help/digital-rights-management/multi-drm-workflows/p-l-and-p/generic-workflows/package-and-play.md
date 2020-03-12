---
description: ExpressPlay의 Bento4 Packager를 사용하여 Primetime Cloud DRM에서 지원하는 모든 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.
seo-description: ExpressPlay의 Bento4 Packager를 사용하여 Primetime Cloud DRM에서 지원하는 모든 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.
seo-title: ExpressPlay Packager / Cloud DRM / TVSDK
title: ExpressPlay Packager / Cloud DRM / TVSDK
uuid: 0d2f5a8d-15c4-42ba-acb8-1dc8d5bc62de
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

ExpressPlay의 Bento4 Packager를 사용하여 Primetime Cloud DRM에서 지원하는 모든 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.

이 작업에서는 타사 도구를 사용하여 보호된 내용을 준비하는 방법에 대해 설명합니다. 이 경우 ExpressPlay *Bento4 도구에서*&#x200B;다양한 DRM 솔루션과 함께 사용할 수 있습니다. 자세한 내용은 ExpressPlay 웹 *사이트의 Bento4 도구* 설명서를 [참조하십시오](https://www.expressplay.com/developer/) .
1. ExpressPlay 계정을 획득하여 ExpressPlay 고객 인증자 정보를 얻습니다.

   Primetime [DRM Cloud 빠른 시작을 참조하십시오.](../../quick-start/quick-overview.md)
1. Primetime 액세스를 위한 콘텐츠를 암호화하는 경우 필요한 인증서(라이선스, 전송 및 패키징 인증서)와 함께 Adobe Primetime Adobe Access SDK를 구입하십시오.
1. DRM 시스템에서 사용할 CEK(Content Encryption Key) 및 CEKSID(Content Encryption Key Storage ID)를 제공합니다. OpenSSL 또는 유사한 기능을 사용하여 임의로 생성합니다.

   CEK 파섹 자체 키 관리 시스템의 자체 서버에 안전하게 저장하거나 ExpressPlay의 [주요 스토리지 솔루션을](https://www.expressplay.com/developer/key-storage/)사용할 수 있습니다.

   CEKSID는 특정 CEK의 식별자입니다. 암호화 키를 전달하지 않습니다(일반적으로). 예를 들어 라이센스 토큰을 요청할 때 CEKSID를 제공합니다.

1. 액세스를 위해 콘텐츠를 암호화하는 경우 CEK를 활용하여 컨텐츠와 연계된 Primetime 액세스 메타데이터를 만드십시오.

1. Bento4 MP4DASH 도구에 맞게 컨텐츠를 *조각하여 준비할 수* 있습니다.

   이 단계에서는 MP4FRAGMENT *도구를 사용할 수* 있습니다. 컨텐츠를 한 번만 조각하면 됩니다. 예:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Bento4 *MPDASH* 툴을 사용하여 &quot;DASH-ify&quot;를 수행하고 조각난 컨텐츠를 암호화합니다.

   이 명령을 사용하여 활용할 모든 DRM 시스템을 지정하고 이전 단계에서 생성된 모든 Primetime 액세스 메타데이터를 전달합니다. 예:

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. &quot;storefront server&quot;를 만듭니다.

       이 서버는 다음 작업을 처리해야 합니다.
   
   1. 고객이 선택한 컨텐츠 이 구현은 클라이언트가 특정 콘텐츠 ID에 대한 콘텐츠 토큰을 요청하기 위한 끝점을 포함해야 합니다.
   1. 고객 권한 부여
   1. 클라이언트의 라이선스 토큰(ExpressPlay) 요청( [ExpressPlay 라이선스 토큰 요청 / 응답 참조](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. 클라이언트를 만듭니다.

   클라이언트는 스토어 서버에 대한 호출을 포함해야 합니다. 사용자가 일부 컨텐츠를 선택한 후 사용자가 인증된 후에 클라이언트가 스토어를 호출하는 것이 좋습니다. 그런 다음 ExpressPlay에서 반환된 토큰을 플레이어로 전달하여 라이선스 요청에 사용합니다. 플레이어의 DRM 구성 요소를 구현하는 방법 소개:

   * HTML5용 브라우저 TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 라이선스 토큰을 통해 클라이언트는 토큰에서 요청 URL을 추출하여 ExpressPlay에 라이선스 요청을 한 다음 사용자를 위해 선택된 보호된 콘텐츠를 재생할 수 있습니다.
