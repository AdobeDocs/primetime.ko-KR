---
seo-title: SWF가 아닌 응용 프로그램 화이트리스트
title: SWF가 아닌 응용 프로그램 화이트리스트
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# SWF가 아닌 응용 프로그램 화이트리스트 {#non-swf-application-whitelisting}

AIR는 애플리케이션 화이트리스트에 적합한 첫 번째 플랫폼이며 비 SWF 애플리케이션(Adobe AIR, iOS, Android 등)을 화이트리스트하는 데 사용하는 속성의 이름입니다. 원래 이름 유지: `policy.allowedAIRApplication.n`. 이를 통해 게시하기 전에 서명 인증서로 서명한 모든 비 Flash 애플리케이션에서 컨텐츠를 재생할 수 있습니다. 이를 *응용 프로그램 ID라고 합니다*. 도구를 사용하여 응용 프로그램 ID를 추출할 수 [!DNL AdobePublisherIDUtility.jar] 있습니다. 이 허용 목록은 Primetime DRM을 지원하는 모든 클라이언트에 적용됩니다.

응용 프로그램 ID는 특정 응용 프로그램에 서명하는 데 사용되는 서명 인증서의 공개 키에서 파생됩니다. 인증서의 공개 키가 만료되면, 이전 인증서로 서명된 앱에서만 재생되는 이전의 모든 콘텐츠가 새 앱에서 재생되지 않습니다(새 인증서로 서명됨).

특정 서명 인증서로 서명된 응용 프로그램에 화이트리스트에 첨부된 컨텐츠 라이브러리가 있고 해당 인증서가 만료되어 새로운 인증서(다른 공개/개인 키 쌍)가 발급되는 경우, 다음 작업을 하지 *않는* 한 이전 내용이 새 응용 프로그램에서 재생되지 않습니다.

* 라이선스 서버 `PolicyUpdateList` 에서 수신 정책을 무시하고 새 서명 인증서의 다이제스트를 사용하여 새 응용 프로그램 화이트 리스트 항목을 삽입합니다.
* 수신 정책을 무시하고 새 응용 프로그램 허용 목록 항목을 삽입하도록 라이센스 서버의 논리를 업데이트합니다.
* 인증서 발급자가 이전 인증서가 사용한 것과 동일한 공용/개인 키 쌍을 사용하는 새 인증서를 발급하도록 요청합니다.
* URL 끝점을 참조하여 URL 끝점을 참조하는 HDS/HLS 콘텐츠를 전달하는 `DRMMetadata`경우, Primetime DRM Java SDK를 `DRMMetadata` 사용하여 DRM 정책을 다시 생성하여 업데이트된 응용 프로그램 화이트 리스트 항목이 포함된 새 DRM 정책을 삽입할 수 있습니다.

* 새로운 서명 인증서의 다이제스트가 포함된 새로운 DRM 정책으로 이전 콘텐츠를 모두 재패키징할 수 있습니다.

자세한 내용은 `policy.allowedAIRApplication.n` 구성 속성 ** 을 참조하십시오.

>[!NOTE]
>
>iOS 응용 프로그램 나열을 허용하려면 특별한 방법이 필요합니다. iOS [프로그래머](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) 용 *TVSDK 안내서의 iOS 애플리케이션*&#x200B;목록 허용 을 참조하십시오.
