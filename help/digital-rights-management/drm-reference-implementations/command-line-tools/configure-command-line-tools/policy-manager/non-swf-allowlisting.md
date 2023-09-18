---
title: 비 SWF 애플리케이션 허용 목록
description: 비 SWF 애플리케이션 허용 목록
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 비 SWF 애플리케이션 허용 목록 {#non-swf-application-isting}

AIR은 SWF이 아닌 애플리케이션(Adobe AIR, iOS, Android 등)을 허용 목록 하는 데 사용하는 속성의 이름과 애플리케이션을 허용하는 첫 번째 플랫폼입니다. 원래 이름을 유지합니다. `policy.allowedAIRApplication.n`. 따라서 게시하기 전에 서명 인증서로 서명된 모든 Flash 이외의 응용 프로그램에서 콘텐츠를 재생할 수 있습니다. 이를 라고 합니다. *애플리케이션 ID*. 다음을 사용하여 애플리케이션 ID를 추출할 수 있습니다. [!DNL AdobePublisherIDUtility.jar] 도구. 이 허용 목록은 Primetime DRM을 지원하는 모든 클라이언트에 적용됩니다.

애플리케이션 ID는 특정 애플리케이션을 서명하는 데 사용되는 서명 인증서의 공개 키에서 파생됩니다. 인증서의 공개 키가 만료된 경우 이전 인증서로 서명된 앱에서만 재생하도록 허용된 모든 이전 콘텐츠는 새 앱(새 인증서로 서명됨)에서 재생되지 않습니다.

특정 서명 인증서로 서명된 애플리케이션에 허용된 콘텐츠 라이브러리가 나열되고 해당 인증서가 만료되고 새 인증서(다른 공개/개인 키 쌍 포함)가 발급되는 경우 이전 콘텐츠가 새 앱에서 재생되지 않습니다 *unless* 다음 중 하나를 수행합니다.

* 사용 `PolicyUpdateList` 들어오는 정책을 재정의하고 새 응용 프로그램 허용 목록 항목을 새 서명 인증서의 다이제스트 로 삽입하려면 라이선스 서버에서 을 하십시오.
* 라이선스 서버의 논리를 업데이트하여 들어오는 정책을 재정의하고 새 응용 프로그램 허용 목록 항목을 삽입합니다.
* 서명 인증서 발급자에게 이전 인증서가 사용한 것과 동일한 공개/개인 키 쌍을 사용하는 새 인증서를 발급하도록 요청합니다.
* 검색할 URL 끝점을 참조하는 HDS/HLS 콘텐츠를 제공하는 경우 `DRMMetadata`, 를 다시 생성할 수 있습니다. `DRMMetadata` (Primetime DRM Java SDK 사용) 업데이트된 애플리케이션 허용 목록 항목이 포함된 새 DRM 정책을 삽입합니다.

* 모든 이전 콘텐츠를 새 서명 인증서의 다이제스트가 있는 새 DRM 정책으로 다시 패키징합니다.

다음을 참조하십시오 `policy.allowedAIRApplication.n` 위치: *구성 속성* 을 참조하십시오.

>[!NOTE]
>
>iOS 애플리케이션을 나열할 수 있도록 허용하려면 특별한 접근 방식이 필요합니다. 다음을 참조하십시오 [iOS 애플리케이션 허용 목록](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 다음에서 *iOS 프로그래머 가이드용 TVSDK*.
