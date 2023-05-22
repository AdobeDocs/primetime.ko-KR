---
description: ExpressPlay에서 제공하는 Primetime DRM Cloud를 사용하여 작업할 때 Safari용 FairPlay를 활성화할 수 있습니다.
title: Safari HLS용 FairPlay 활성화
exl-id: 761c7cb8-3068-44c9-8ceb-6411c509c0a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Safari HLS용 FairPlay 활성화 {#enable-fairplay-for-safari-hls}

ExpressPlay에서 제공하는 Primetime DRM Cloud를 사용하여 작업할 때 Safari용 FairPlay를 활성화할 수 있습니다.

다음 사항이 있는지 확인합니다.

* HLS 비디오를 재생할 수 있는 작동하는 샘플 앱입니다.

   샘플 앱은 ExpressPlay에서 제공하는 Primetime DRM을 통해 처리되는 라이선스로 FairPlay로 보호된 콘텐츠를 재생할 수 있어야 합니다.
* FairPlay 보호 기능이 포함된 샘플 HLS 콘텐츠(M3U8 매니페스트)입니다.

여기에서 이 정보를 최대한 활용하려면 하위 섹션으로 시작하는 다중 DRM 워크플로우에 대해 알아보십시오 [참조 서버: 샘플 ExpressPlay 권한 서버(SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) Multi-DRM 워크플로우 안내서에서 다음을 수행합니다. 먼저 권한 부여 및 키 서버를 설정하는 방법에 대한 설명서를 읽고 아래 정보가 훨씬 유용합니다.
다음 항목이 필요합니다.

* 사용자 *production* ExpressPlay의 고객 인증자
* 동일한 콘텐츠 키 및 `iv` 콘텐츠가 패키지화된 대상.
* FairPlay 공개 키 인증서의 위치입니다.

FairPlay/Safari 앱을 수정하려면:

1. FairPlay 라이선스 서버 요청에 사용된 FairPlay 공개 키 인증서의 위치를 설정합니다.

   예:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 수동 FairPlay 라이센스 수행 *토큰* 라이선스 토큰 URL을 얻기 위해 ExpressPlay에 요청합니다.

       다음 방법 중 하나로 이 단계를 완료할 수 있습니다.
   
   * ExpressPlay 프로덕션 고객 인증자를 사용하십시오.
   * 동일한 콘텐츠 키 사용 및 `iv` 이 요청에서 재생할 콘텐츠를 패키지하는 데 사용되었습니다.

      셸에서 다음 명령을 실행하고 ExpressPlay 고객 인증자로 대체하여 샘플 콘텐츠에 대한 라이선스 토큰 URL을 얻습니다.

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      라이선스 토큰 URL이 포함된 응답은 다음과 같습니다.

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. ExpressPlay에서 라이선스 토큰 URL을 사용하여 변수를 설정합니다.

   예:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. 앱에서 보호된 콘텐츠를 재생하려면 먼저 콘텐츠의 URL 체계를 `skd://` 끝 `https://`.

   재생을 허용하는 라이선스 서버를 호출하기 전에 앱에 이 URL 체계 변경 내용을 추가해야 합니다.

   키 관리 시스템의 콘텐츠 키에 대한 액세스를 제공하는 콘텐츠 ID가 `skd://` 프로토콜. 플레이어가 보호된 콘텐츠를 재생하기 위한 라이센스를 받을 준비가 되면 먼저 ExpressPlay 라이센스 서버와 통신하기 위해 프로토콜을 전환해야 합니다. 아래 예에서는 `myServerProcessSPCPath` 은(는) 라이선스 서버 요청에 대한 올바른 URL 체계를 포함하도록 수정되었습니다.

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
