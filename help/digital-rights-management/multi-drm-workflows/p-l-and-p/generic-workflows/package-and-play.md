---
description: ExpressPlay의 Bento4 패키지를 사용하여 ExpressPlay에서 제공하는 Primetime Cloud DRM에서 지원하는 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.
title: ExpressPlay Packager / Cloud DRM / TVSDK
exl-id: ff937279-3866-4d0a-9a19-cf61726299e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

ExpressPlay의 Bento4 패키지를 사용하여 ExpressPlay에서 제공하는 Primetime Cloud DRM에서 지원하는 DRM 솔루션에 대한 콘텐츠를 준비할 수 있습니다.

이 작업에서는 서드파티 도구를 사용하여 보호된 콘텐츠(이 경우)를 준비하는 방법을 설명합니다 *ExpressPlay Bento4 도구*&#x200B;다양한 DRM 솔루션과 함께 사용할 수 있습니다. 자세한 내용은 *Bento4 도구* 에 대한 설명서 [익스프레스 플레이](https://www.expressplay.com/developer/) 웹 사이트.
1. ExpressPlay 계정을 획득하고 ExpressPlay 고객 인증자 정보를 얻습니다.

   다음을 참조하십시오 [Primetime DRM 클라우드 빠른 시작.](../../quick-start/quick-overview.md)
1. Primetime 액세스용 콘텐츠를 암호화하는 경우 필요한 인증서(라이선스, 전송 및 패키징 인증서)와 함께 Adobe에서 Primetime Adobe 액세스 SDK를 획득하십시오.
1. DRM 시스템에서 사용할 CEK(콘텐츠 암호화 키) 및 CEKSID(콘텐츠 암호화 키 저장소 ID)를 제공합니다. (OpenSSL 또는 이와 유사한 기능을 사용하여 임의로 생성합니다.)

   CEK는 비디오 파일을 암호화하는 데 사용하는 실제 키입니다. 자체 키 관리 시스템의 서버에 안전하게 저장하거나 ExpressPlay의 [주요 스토리지 솔루션](https://www.expressplay.com/developer/key-storage/).

   CEKSID는 특정 CEK에 대한 식별자입니다. 암호화 키를 전달하지 않습니다(일반적으로). 예를 들어 라이센스 토큰을 요청할 때 CEKSID를 제공합니다.

1. 액세스용 콘텐츠를 암호화하는 경우 CEK를 활용하여 콘텐츠와 연결된 Primetime Access 메타데이터를 만드십시오.

1. 콘텐츠를 조각화하여 다음을 위한 준비: *Bento4 MP4DASH* 도구.

   이 단계에서는 다음을 사용할 수 있습니다. *MP4FRAGMENT* 도구. 콘텐츠를 한 번만 조각화하면 됩니다. 예:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. 사용 *Bento4 MPDASH* &quot;DASH-ify&quot; 도구를 사용하여 단편화된 콘텐츠를 암호화합니다.

   이 명령을 사용하여 활용할 모든 DRM 시스템을 지정하고 이전 단계에서 생성된 Primetime Access 메타데이터를 전달합니다. 예:

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

1. &quot;storefront 서버&quot;를 만듭니다.

       이 서버는 다음 작업을 처리해야 합니다.
   
   1. 고객이 콘텐츠를 선택합니다. 이 구현에는 클라이언트가 특정 콘텐츠 ID에 대한 콘텐츠 토큰을 요청할 수 있는 엔드포인트가 포함되어야 합니다.
   1. 고객 권한
   1. 클라이언트의 라이센스 토큰(ExpressPlay) 요청( [ExpressPlay 라이선스 토큰 요청/응답 참조](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. 클라이언트를 만듭니다.

   클라이언트에는 Storefront 서버에 대한 호출이 포함되어야 합니다. Adobe은 사용자가 일부 콘텐츠를 선택한 후, 사용자가 인증된 후에 클라이언트가 상점 첫 페이지를 호출하는 것을 권장합니다. 그런 다음 ExpressPlay에서 반환된 토큰을 플레이어에 전달하여 라이센스 요청에 사용합니다. 플레이어의 DRM 구성 요소 구현에 대한 소개는 다음과 같습니다.

   * HTML 5용 브라우저 TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 이제 라이선스 토큰을 사용하여 클라이언트는 토큰에서 요청 URL 을 파생하고 ExpressPlay에 라이선스 요청을 한 다음 사용자에 대해 선택한 보호된 콘텐츠를 재생할 수 있습니다.
