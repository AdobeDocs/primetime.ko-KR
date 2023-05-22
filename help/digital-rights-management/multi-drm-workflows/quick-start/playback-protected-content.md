---
description: DRM 솔루션을 테스트하려면 작업 중인 특정 DRM 솔루션을 처리할 수 있는 비디오 애플리케이션이 필요합니다. 이 플레이어는 Adobe 또는 고유한 TVSDK 기반 비디오 애플리케이션에서 사용할 수 있는 샘플 플레이어일 수 있습니다.
title: 보호된 콘텐츠 재생
exl-id: b0e09474-f752-495f-a702-93f288535403
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 보호된 콘텐츠 재생 {#playback-your-protected-content}

DRM 솔루션을 테스트하려면 작업 중인 특정 DRM 솔루션을 처리할 수 있는 비디오 애플리케이션이 필요합니다. 이 플레이어는 Adobe 또는 고유한 TVSDK 기반 비디오 애플리케이션에서 사용할 수 있는 샘플 플레이어일 수 있습니다.

1. ExpressPlay 서버에서 받은 토큰 응답의 라이선스 서버 URL을 사용하여 보호된 콘텐츠를 재생할 수 있는지 테스트합니다.

   * **와이드빈** - ExpressPlay 라이선스 토큰 요청에서 받은 대로 Widevine 응답을 바로 사용합니다.
   * **PlayReady** - 라이선스 토큰 요청에서 반환된 JSON 개체에서 라이선스 서버 URL 및 토큰을 가져옵니다.
   * **페어플레이** - ExpressPlay 라이선스 토큰 요청에서 받은 대로 FairPlay 응답을 바로 사용합니다.

1. 자체 플레이어 또는 기존 Adobe 샘플 플레이어를 사용하여 보호된 콘텐츠의 재생을 테스트합니다.

   보호된 콘텐츠의 URL(테스트 중인 DRM 솔루션에 따라 M3U8 또는 MPD 매니페스트의 위치)을 제공합니다.

   테스트하는 플레이어에서 제공하는 인터페이스에 따라 라이선스 URL과 토큰을 입력 필드의 문자열로 분리하거나, 텍스트 상자에 붙여 넣은 JSON 개체로 제공하거나, URL의 쿼리 매개 변수로 제공하라는 메시지가 표시될 수 있습니다.

   테스트 플레이어의 몇 가지 가능성이 여기에 나열됩니다.

   * HTML5 참조 플레이어:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka 플레이어:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * 샘플 TVSDK 플레이어(개발 중) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **FairPlay 설정을 테스트할 때 재생 확인:** ExpressPlay 라이선스 서버를 사용할 때 콘텐츠를 재생하려면 FairPlay에 몇 가지 추가 단계가 필요합니다. 을 사용하는 경우 [!DNL curl] 연결을 테스트하려면에 설명된 대로 [라이선스](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), 다음을 수행해야 합니다. *M3U8 매니페스트 편집* (패키지된 콘텐츠) 다음과 같습니다.

1. 라이선스 토큰 요청에서 다시 받은 응답을 `#EXT-X-KEY:` 매니페스트의 태그; 및
1. 응답(현재 매니페스트에 있음)에서, 의 해당 URL의 프로토콜을 변경합니다. `https://` 끝 `skd://`.

   다음은 라이센싱 단계를 포함하여 FairPlay로 재생을 테스트하는 전체 예입니다.

1. FairPlay 라이선스 토큰 요청을 사용하여 라이선스 토큰 URL을 받으십시오. (자체 프로덕션 고객 인증자를 사용하고 동일한 CEK 및 `iv` FairPlay 콘텐츠를 패키지하는 데 사용되었습니다.) 다음 명령을 실행하여 예제 컨텐츠에 대한 라이선스 토큰 URL을 얻습니다.

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   다음과 같은 라이선스 토큰 URL을 사용하여 응답을 다시 받아야 합니다.

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 반환된 라이선스 토큰 URL 응답을 M3U8 매니페스트에 추가하고 *라이선스 토큰 URL 체계를 다음으로 변경* `sdk://` 출처: `https://`. 다음은 M3U8 매니페스트에 있는 #EXT-X-KEY 태그의 예입니다.

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >위의 정보는 FairPlay 설정의 테스트에만 적용됩니다. FairPlay 핸들러를 구성하는 방법에 따라 프로덕션 설정에는 적용되지 않을 수 있습니다. 다음을 참조하십시오 [iOS 애플리케이션에서 Apple FairPlay 활성화](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) 을 참조하십시오.

비디오가 재생되는 경우 콘텐츠를 정상적으로 패키징하고 라이선스를 취득했습니다. 비디오가 재생되지 않는 경우 문제 해결 페이지에서 몇 가지 문제 해결 방법을 확인하십시오.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

예를 들어 위에 나열된 첫 번째 테스트 플레이어의 UI 부분에서는 ExpressPlay 서버에서 얻은 라이선스 정보를 제공합니다.

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
