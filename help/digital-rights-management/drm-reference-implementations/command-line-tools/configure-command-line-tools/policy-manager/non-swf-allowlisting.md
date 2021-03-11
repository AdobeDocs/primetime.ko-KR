---
title: SWF가 아닌 응용 프로그램 목록 허용
description: SWF가 아닌 응용 프로그램 목록 허용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# SWF가 아닌 응용 프로그램에서 {#non-swf-application-isting} 나열 허용

AIR는 SWF가 아닌 응용 프로그램 허용 목록에 사용하는 속성 이름(Adobe AIR, iOS, Android 등)과 목록을 포함하는 첫 번째 플랫폼입니다. 원래 이름 유지:`policy.allowedAIRApplication.n`. 이를 통해 게시하기 전에 서명 인증서로 서명된 모든 Flash이 아닌 애플리케이션에서 컨텐츠를 재생할 수 있습니다. 이를 *응용 프로그램 ID*&#x200B;라고 합니다. [!DNL AdobePublisherIDUtility.jar] 도구를 사용하여 응용 프로그램 ID를 추출할 수 있습니다. 이 허용 목록은 Primetime DRM을 지원하는 모든 클라이언트에 적용됩니다.

응용 프로그램 ID는 특정 응용 프로그램을 서명하는 데 사용되는 서명 인증서의 공개 키에서 파생됩니다. 인증서의 공개 키가 만료되면 이전 인증서로 서명된 앱에서만 나열된 모든 이전 콘텐츠가 재생되도록 허용되면 새 앱에서 재생되지 않습니다(새 인증서로 서명됨).

콘텐트 라이브러리가 특정 서명 인증서로 서명된 응용 프로그램에 나열되고 해당 인증서가 만료되어 다른 공개/비공개 키 쌍 사용 권한이 있는 새 인증서가 발급되는 경우, 다음 작업 중 하나를 수행하지 않으면 이전 내용이 새 응용 프로그램 *에서 재생되지 않습니다.*

* 라이센스 서버에서 `PolicyUpdateList`을(를) 사용하여 수신 정책을 재정의하고 새 서명 인증서의 다이제스트에 새 응용 프로그램 허용 목록 항목을 삽입합니다.
* 들어오는 정책을 무시하고 새 응용 프로그램 허용 목록 항목을 삽입하도록 라이센스 서버의 논리를 업데이트합니다.
* 서명 인증서 발급자가 이전 인증서가 사용한 것과 동일한 공용/개인 키 쌍을 사용하는 새 인증서를 발급하도록 요청합니다.
* `DRMMetadata`을(를) 검색하기 위해 URL 끝점을 참조하는 HDS/HLS 콘텐츠를 배포하는 경우 `DRMMetadata`(Primetime DRM Java SDK 사용)을 다시 생성하여 업데이트된 응용 프로그램 허용 목록 항목이 포함된 새 DRM 정책을 삽입할 수 있습니다.

* 새로운 서명 인증서의 다이제스트가 포함된 새로운 DRM 정책으로 이전 콘텐츠를 모두 재패키징할 수 있습니다.

자세한 내용은 *구성 속성*&#x200B;의 `policy.allowedAIRApplication.n`을 참조하십시오.

>[!NOTE]
>
>iOS 애플리케이션 목록을 허용하려면 특별한 접근 방식이 필요합니다. iOS Programmer&#39;s Guide *의* TVSDK에서 [iOS 응용 프로그램 허용 목록](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md)을 참조하십시오.
