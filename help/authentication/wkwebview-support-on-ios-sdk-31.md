---
title: iOS SDK 3.1+에 대한 WKWebView 지원
description: iOS SDK 3.1+에 대한 WKWebView 지원
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# iOS SDK 3.1+에 대한 WKWebView 지원 {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>

**Apple은 iOS에서 UIWebView를 사용하지 않으므로 WKWebView에 대한 지원을 통해 iOS SDK 3.1을 업데이트했습니다.**

## 호환성 {#compatibility}

iOS SDK 버전 3.1부터 구현자는 이제 WKWebView 또는 UIWebView를 서로 교환하여 사용할 수 있습니다. UIWebView는 Apple에서 더 이상 사용되지 않으므로 앱은 향후 iOS 버전에 대한 문제를 방지하기 위해 WKWebView로 마이그레이션해야 합니다.

마이그레이션은 WKWebView를 사용하여 UIWebView 클래스를 단순히 전환하는 것을 의미하며, Adobe의 AccessEnabler에 대해 수행할 특정 작업은 없습니다.

## 알려진 문제 {#known-issues}

Adobe의 AccessEnabler가 숨겨진 내부 UIWebView 인스턴스를 사용하여 &quot;[수동 인증](/help/authentication/sso-passive-authn.md)&quot;(특정 MVPD에 대해) &quot;수동&quot; 흐름은 각 요청자 ID에 대한 인증이 필요한 MVPD에 유용하며, 이 흐름에서 SSO(Adobe SSO)를 시뮬레이션하기 위해 여러 iOS 애플리케이션에서 동일한 팀 ID를 사용한 프로그래머에게 이득을 주었습니다. 이 기능은 현재 제한된 수의 MVPD에서 사용됩니다.

이 기능은 Adobe이 인증 쿠키를 캡처하고 &quot;수동&quot; 흐름 중에 재생하도록 허용하는 UIWebView의 동작을 사용했습니다. WKWebView는 Adobe이 로그인 시 설정된 쿠키를 캡처하고 WKWebView의 숨겨진 인스턴스를 사용하여 이를 재생하지 못하도록 하는 강력한 보안을 도입합니다. 이러한 보안 개선 사항으로 인해 &quot;수동&quot; 흐름만 매우 제한된 MVPD 집합(동일한 팀 ID를 사용하는 여러 응용 프로그램)만 혜택을 받았음을 고려하여 Adobe은 웹 보기를 사용하여 MVPD에 대한 &quot;수동 인증&quot; 기능을 제거함으로써 인증을 수행했습니다.

SFSsafariViewController를 사용하도록 구성된 MVPD에 대해서는 이 기능이 여전히 제공되지만, 이 경우 SFSsafariViewController를 &quot;숨김&quot; 방식으로 사용할 수 없으므로 &quot;수동&quot; 인증이 사용자에게 표시됩니다.
