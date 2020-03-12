---
description: DRM 솔루션을 테스트하려면 작업 중인 특정 DRM 솔루션을 처리할 수 있는 비디오 애플리케이션이 필요합니다. 이 플레이어는 Adobe에서 제공하는 샘플 플레이어 또는 TVSDK 기반의 비디오 애플리케이션이 될 수 있습니다.
seo-description: DRM 솔루션을 테스트하려면 작업 중인 특정 DRM 솔루션을 처리할 수 있는 비디오 애플리케이션이 필요합니다. 이 플레이어는 Adobe에서 제공하는 샘플 플레이어 또는 TVSDK 기반의 비디오 애플리케이션이 될 수 있습니다.
seo-title: 보호된 콘텐츠 재생
title: 보호된 콘텐츠 재생
uuid: 84f73ee7-43d0-481c-a5e7-14f92169323c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 보호된 콘텐츠 재생 {#playback-your-protected-content}

DRM 솔루션을 테스트하려면 작업 중인 특정 DRM 솔루션을 처리할 수 있는 비디오 애플리케이션이 필요합니다. 이 플레이어는 Adobe에서 제공하는 샘플 플레이어 또는 TVSDK 기반의 비디오 애플리케이션이 될 수 있습니다.

1. ExpressPlay 서버에서 수집한 토큰 응답의 라이선스 서버 URL을 사용하여 보호된 내용을 재생할 수 있는지 테스트합니다.

   * **Widevine** - ExpressPlay 라이선스 토큰 요청에서 수신한 대로 직접 Widevine 응답을 사용합니다.
   * **PlayReady** - 라이선스 토큰 요청에서 반환된 JSON 개체에서 라이선스 서버 URL과 토큰을 가져옵니다.
   * **FairPlay** - ExpressPlay 라이선스 토큰 요청에서 수신한 대로 바로 FairPlay 응답을 사용합니다.

1. 자신의 플레이어 또는 기존 Adobe 샘플 플레이어를 사용하여 보호된 콘텐츠의 재생을 테스트할 수 있습니다.

   보호된 콘텐츠에 대한 URL을 제공합니다(테스트 중인 DRM 솔루션에 따라 M3U8 또는 MPD 매니페스트 위치).

   테스트할 플레이어에서 제공한 인터페이스에 따라 라이선스 URL과 토큰을 입력 필드의 문자열로 구분하거나 텍스트 상자에 붙여 넣은 JSON 개체나 URL의 쿼리 매개 변수로 제공하도록 요청을 받을 수 있습니다.

   테스트 플레이어에 대한 몇 가지 가능성은 다음과 같습니다.

   * HTML5 참조 플레이어:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * 샘플 TVSDK 플레이어(개발 중) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **FairPlay 설정을 테스트할 때 재생 확인:** FairPlay 라이선스 서버를 사용하는 경우 ExpressPlay에서 컨텐츠를 재생하려면 추가 단계가 필요합니다. 연결을 테스트하는 [!DNL curl] 데 사용하는 경우(라이센스에 [설명된 대로](../../multi-drm-workflows/quick-start/handle-the-licensing.md)) 다음과 같이 M3U8 매니페스트 *(패키징된 컨텐츠)를* 편집해야 합니다.

1. 라이선스 토큰 요청에서 돌아온 응답을 매니페스트의 `#EXT-X-KEY:` 태그에 추가합니다.and
1. 응답에서 이제 매니페스트에 있는 URL의 프로토콜을 `https://` 로 변경합니다 `skd://`.

   다음은 라이선스 단계를 비롯하여 FairPlay를 사용하여 재생을 테스트하는 전체 예입니다.

1. FairPlay 라이선스 토큰 요청을 사용하여 라이선스 토큰 URL을 얻습니다. (직접 만든 프로덕션 고객 인증자를 사용하고 FairPlay 컨텐츠를 패키지하는 데 사용된 동일한 CEK를 사용해야 `iv` 합니다.) 다음 명령을 실행하여 예제 컨텐츠에 대한 라이센스 토큰 URL을 가져옵니다.

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   다음과 같은 라이선스 토큰 URL로 다시 응답해야 합니다.

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 반환된 라이선스 토큰 URL 응답을 M3U8 매니페스트에 입력하고 라이선스 토큰 URL의 체계를 *에서* 로 `sdk://` 변경합니다 `https://`. 다음은 M3U8 매니페스트에서 #EXT-X-KEY 태그의 예입니다.

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE] {importance=&quot;high&quot;}
   >
   >앞의 정보는 FairPlay 설정의 테스트에만 적용됩니다. FairPlay 핸들러를 구성하는 방법에 따라 프로덕션 설정에 적용되지 않을 수 있습니다. 자세한 [내용은 iOS 애플리케이션에서](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) Apple FairPlay 활성화를 참조하십시오.

비디오가 재생되는 경우 콘텐츠를 성공적으로 패키징하고 라이선스를 부여받게 됩니다. 비디오가 재생되지 않는 경우 문제 해결 페이지에서 문제 해결 방법을 확인하십시오.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

예를 들어, 다음은 위에 나열된 첫 번째 테스트 플레이어에서 UI의 일부이며 ExpressPlay 서버에서 얻은 라이센스 정보를 제공합니다.

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
