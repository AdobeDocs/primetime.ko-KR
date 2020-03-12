---
description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 작업할 때 Safari용 FairPlay를 활성화할 수 있습니다.
seo-description: ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 작업할 때 Safari용 FairPlay를 활성화할 수 있습니다.
seo-title: Safari HLS 파섹
title: Safari HLS 파섹
uuid: 6a250a31-cc4b-4c4b-b1e9-893ee3ca5d78
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Safari HLS 파섹 {#enable-fairplay-for-safari-hls}

ExpressPlay 기반의 Primetime DRM Cloud를 사용하여 작업할 때 Safari용 FairPlay를 활성화할 수 있습니다.

다음을 확인하십시오.

* HLS 비디오를 재생할 수 있는 기능 샘플 앱.

   샘플 앱은 ExpressPlay에서 제공하는 Primetime DRM을 통해 처리된 라이선스로 FairPlay로 보호된 콘텐츠를 재생할 수 있어야 합니다.
* FairPlay 보호와 함께 패키지화된 샘플 HLS 컨텐츠(M3U8 매니페스트)

여기에서 정보를 완전히 사용하려면 하위 섹션 참조 서버부터 시작하는 다중 DRM 워크플로우에 대해 [알아봅니다.Sample ExpressPlay Entitlement Server (SEE)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) in the Multi-DRM Workflows guide. 먼저 권한 부여 및 키 서버를 설정하는 방법에 대한 설명서를 읽고 아래 정보가 훨씬 유용할 것입니다.
다음 항목이 필요합니다.

* ExpressPlay의 *프로덕션* 고객 인증자
* 컨텐츠가 패키지된 동일한 컨텐츠 `iv` 키입니다.
* FairPlay 공개 키 인증서의 위치입니다.

FairPlay/Safari 앱을 수정하려면:

1. FairPlay 라이선스 서버 요청에 사용된 FairPlay 공개 키 인증서의 위치를 설정합니다.

   예:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 라이센스 토큰 URL을 얻으려면 ExpressPlay에 수동 FairPlay 라이선스 *토큰* 요청을 수행하십시오.

       다음 방법 중 하나로 이 단계를 완료할 수 있습니다.
   
   * ExpressPlay 제작 고객 인증기를 사용하십시오.
   * 재생할 콘텐트를 패키징하는 데 사용된 동일한 콘텐츠 키와 이 `iv` 요청에서 동일한 콘텐츠 키를 사용하십시오.

      셸에서 다음 명령을 실행하고 ExpressPlay 고객 인증자로 대체하여 샘플 컨텐츠의 라이선스 토큰 URL을 얻습니다.

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      라이선스 토큰 URL이 있는 응답은 다음과 같습니다.

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. ExpressPlay에서 라이선스 토큰 URL로 변수를 설정합니다.

   예:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. 앱에서 보호된 콘텐츠를 재생하려면 먼저 콘텐츠의 URL 체계를 에서 `skd://` 로 변경하십시오 `https://`.

   재생을 허용하는 라이선스 서버에 대한 호출 전에 앱에서 이 URL 체계 변경을 추가해야 합니다.

   키 관리 시스템의 컨텐츠 키에 대한 액세스를 제공하는 컨텐츠 ID가 `skd://` 프로토콜과 함께 M3U8 매니페스트에 패키지되어 있으므로 프로토콜을 변경해야 합니다. 보호된 내용을 재생할 수 있는 라이선스를 받을 준비가 되면 ExpressPlay 라이선스 서버와 통신하려면 먼저 프로토콜을 전환해야 합니다. 아래 예에서 라이센스 서버 요청에 대한 올바른 URL 체계를 포함하도록 `myServerProcessSPCPath` 수정되었습니다.

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```

