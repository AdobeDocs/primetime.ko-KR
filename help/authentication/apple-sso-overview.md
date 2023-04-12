---
title: Apple SSO 개요
description: Apple SSO 개요
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---



# Apple SSO 개요 {#apple-sso-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#Introduction}

Apple은 사람들이 장치 시스템 수준에서 TV 공급자 계정에 로그인할 수 있도록 해주는 API를 제공하여 앱 별로 인증하지 않아도 됩니다.

따라서 Apple 및 Adobe Primetime 인증은 iPhone, iPad 및 Apple TV 소유자를 위한 TV Everywhere 에코시스템에서 플랫폼 SSO(Single Sign-On) 사용자 경험을 만들기 위해 파트너 관계를 맺고 있습니다.

Apple 장치에서 SSO(Single Sign-On) 사용자 환경을 활용하려면 사전 요구 사항 목록을 완료해야 합니다.

</br>

## 전제 조건 {#Prerequisites}

프로그래머, MVPD, Adobe Primetime 인증 또는 Apple과 같이 TVE 사업과 관련된 하나 이상의 업체에 사전 요구 사항이 적용될 수 있습니다.

</br>

### 프로그래머 {#Programmer}

SSO(Single Sign-On) 사용자 환경을 활용하려면 하나의 프로그래머가 다음을 수행해야 합니다.

1. Xcode 버전 8 및 iOS/tvOS 버전 10 이상을 사용하십시오.

1. 다음 정보 [비디오 가입자 단일 사인온 권한](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) Apple 개발자 계정에 구성 활성화하려면 Apple에 문의하십시오 [비디오 가입자 계정 프레임워크](https://developer.apple.com/documentation/videosubscriberaccount) Apple 팀 ID용.

1. 를 통해 원하는 각 통합(채널 x MVPD)과 원하는 플랫폼(iOS/tvOS)에 대해 단일 사인온(예)을 활성화합니다 [Adobe Primetime TVE 대시보드](https://console.auth.adobe.com/).

1. Adobe Primetime 인증 팀에서 제공하는 다음 두 솔루션 중 하나를 사용하여 Apple SSO 워크플로우를 통합합니다.

   - Adobe Primetime Authentication REST API는 iOS, iPadOS 또는 tvOS에서 실행되는 클라이언트 애플리케이션의 최종 사용자에 대해 플랫폼 SSO(Single Sign-On) 인증을 지원할 수 있습니다. 다음을 참조하십시오 [Apple SSO Cookbook(REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK는 iOS, iPadOS 또는 tvOS에서 실행되는 클라이언트 애플리케이션의 최종 사용자를 위해 플랫폼 SSO(Single Sign-On) 인증을 지원할 수 있습니다. 다음을 참조하십시오 [Apple SSO Cookbook(iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>Pro 팁:</u>** 사용자의 구독 정보에 액세스하려면 사용자가 장치의 카메라 또는 마이크에 대한 액세스를 제공하는 것과 같이 계속 진행할 수 있도록 애플리케이션 권한을 부여해야 합니다. 응용 프로그램별로 이 권한을 요청해야 하며 장치가 사용자의 선택을 저장합니다. 사용자는 애플리케이션 설정(TV 공급자 권한 액세스)이나 *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* tvOS에서

   - **<u>Pro 팁:</u>** 애플리케이션이 전경 상태가 되면 사용자의 권한을 요청하는 것이 좋지만, 애플리케이션이 확인할 수 있으므로 이것은 제안일 뿐입니다 [액세스 권한](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 사용자 인증을 요구하기 전에 언제든지 사용자의 구독 정보를 볼 수 있습니다. 또한 AccessEnabler iOS/tvOS SDK API는 필요할 때 사용자 권한을 자동으로 요청합니다.

   - **<u>Pro 팁:</u>** SSO(Single Sign-On) 사용자 환경의 이점을 설명하여 구독 정보에 액세스할 수 있는 권한을 부여하지 않는 사용자에게 인센티브를 제공하는 것이 좋습니다. 사용자는 애플리케이션 설정(TV 공급자 권한 액세스)이나 *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* tvOS에서

따라서 다음 사용자 흐름과 부합하는 경험을 만들어야 하며, 이 경우 애플리케이션 개발을 시작하기 전에 참조할 것을 권장합니다.

- [iPhone / iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) 사용자 흐름
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) 사용자 흐름


>[!IMPORTANT]
>
> 단일 사인온 기능이 **활성화됨** iOS/tvOS용 **및** Apple의 경우 **온보딩(지원됨) 또는 피커** Apple SSO 워크플로우에서 인증/로그아웃 흐름에는 Apple 및 Adobe Primetime 인증 솔루션이 모두 포함되지만 다른 모든 흐름(인증, 사전 인증, 메타데이터 등)은 모두 포함됩니다. 은 Adobe Primetime 인증으로만 제공됩니다.


>[!IMPORTANT]
>
> 단일 사인온 기능이 **비활성화됨** iOS/tvOS용 **또는** Apple의 경우 **온보딩되지 않음(지원되지 않음)** MVPD는 인증/로그아웃 플로우를 Apple SSO 워크플로우에서 Adobe Primetime 인증으로만 서비스되는 일반 워크플로우로 대체됩니다.


>[!IMPORTANT]
>
> Apple SSO 워크플로우의 한 가지 주요 이득 은 하나의 화면 인증 사용자 흐름으로 표시되며, 단일 사인온 기능이 있을 때 Apple TV에서 제공할 수도 있습니다 **활성화됨** tvOS용 **및** Apple의 경우 **온보딩(지원됨)** MVPD


### MVPD {#MVPD}

SSO(Single Sign-On) 사용자 환경을 활용하려면 하나의 MVPD가 다음을 수행해야 합니다.

 

1. Apple 측에서 Apple SSO 워크플로우로 온보딩됩니다. 온보딩 프로세스를 용이하게 하려면 Apple에 문의하십시오.
1. 사용자 로그인 양식을 처리할 수 있는 JavaScript TVML 애플리케이션을 제공합니다. 적절한 설명서를 받으려면 Apple에 문의하십시오.
1. 온보딩 프로세스 중에 Apple에서 지정한 공급자 식별자를 나타내는 문자열 값을 제공합니다. 구성 변경을 수행하려면 Adobe Primetime 인증에 문의하십시오.

</br>

## FAQ {#FAQ}

1. Apple SSO 워크플로우에서 문제가 발생하는 경우 AccessEnabler iOS/tvOS SDK를 사용하는 애플리케이션에서 일반 인증 흐름을 폴백할 수 있습니까?
   - 이 작업은 가능하지만, [Adobe Primetime TVE 대시보드](https://console.auth.adobe.com/). 다음 *단일 사인온 활성화* 을(를) 설정해야 합니다. *아니요* 원하는 통합(채널 x MVPD)과 원하는 플랫폼(iOS/tvOS)에 대해 을 참조하십시오.
   - 애플리케이션이 를 호출한 후에만 구성 변경을 승인합니다 [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) AccessEnabler iOS/tvOS SDK를 사용하는 경우 API입니다.
1. 다른 장치 또는 다른 애플리케이션에서 플랫폼 SSO를 통해 로그인하여 인증이 발생한 시점을 애플리케이션이 알 수 있습니까?
   - 이 정보는 사용할 수 없습니다.
1. 동일한 장치에서 플랫폼 SSO를 통해 로그인하여 인증이 발생한 시점을 애플리케이션이 알 수 있습니까? 
   - 이 정보는 사용자 메타데이터 키의 일부로 사용할 수 있습니다. *tokenSource*: 문자열 값을 반환해야 합니다. 이 경우 &quot;Apple&quot;.
1. 사용자가 로 이동하여 로그인하면 어떻게 됩니까? *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* 애플리케이션과 통합되지 않은 MVPD를 사용하는 tvOS 섹션
   - 사용자가 애플리케이션을 시작하면 Apple SSO 워크플로우를 통해 사용자를 인증하지 않습니다. 따라서 애플리케이션은 일반 인증 플로우에 폴백하고 자체 MVPD 선택기를 제공해야 합니다.
1. 사용자가 로 이동하여 로그인하면 어떻게 됩니까? *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* MVPD를 사용하는 tvOS 섹션 *단일 사인온 활성화* 설정 *아니요* on [Adobe Primetime TVE 대시보드](https://console.auth.adobe.com/) iOS/tvOS 플랫폼용
   - 사용자가 애플리케이션을 시작하면 Apple SSO 워크플로우를 통해 사용자를 인증하지 않습니다. 따라서 애플리케이션은 일반 인증 플로우에 폴백하고 자체 MVPD 선택기를 제공해야 합니다.
1. Apple에서 지원하지 않는 온보딩되지 않지만 Apple 선택기에 있는 MVPD가 사용자에게 있으면 어떻게 됩니까?
   - 사용자가 애플리케이션을 시작하면 인증 흐름을 완료하지 않고 Apple SSO 워크플로우를 통해서만 MVPD를 선택합니다. 따라서 애플리케이션은 일반 인증 플로우에 대비해야 하지만 이미 선택한 MVPD를 사용할 수 있습니다.
1. Apple에서 지원하지 않는(지원되지 않음) MVPD가 사용자에게 있으면 어떻게 됩니까?
   - 사용자가 애플리케이션을 시작하면 Apple SSO 워크플로우를 통해 &quot;다른 TV 공급자&quot; 선택기 옵션을 선택합니다. 따라서 애플리케이션은 일반 인증 플로우에 폴백하고 자체 MVPD 선택기를 제공해야 합니다.
1. 사용자가 다음 미디어 중 하나를 통해 성능이 저하되는 MVPD를 가지고 있으면 어떻게 됩니까? [Adobe Primetime TVE 대시보드](https://console.auth.adobe.com/)?
   - 사용자가 애플리케이션을 시작하면 사용자는 Apple SSO 워크플로우를 통해 인증되지 않고 저하 메커니즘을 통해 인증됩니다.
   - 이 환경은 사용자에게 매끄러운 상태여야 하며 응용 프로그램은 *N010* AccessEnabler iOS/tvOS SDK를 사용하는 경우 경고 코드입니다.
1. MVPD 사용자 ID가 Apple SSO와 비Apple SSO 인증 흐름 간에 변경됩니까?
   - 사용자 ID는 변경되지 않지만 선택한 각 공급자에 대해 확인되어야 합니다. 
1. 인증 TTL에 변경 사항이 있습니까?
   - Adobe Primetime 인증은 프로그래머가 각 MVPD와 통합하는 데 필요한 TTL을 계속 준수합니다.
   - 한 Programmer 응용 프로그램에서 Apple SSO를 통해 다른 Programmer 응용 프로그램으로 이동할 때 두 번째 응용 프로그램은 해당 Programmer x MVPD 통합의 TTL을 갖습니다(인증을 받는 첫 번째 응용 프로그램의 TTL을 공유하지 않음)

|  | Adobe Primetime 인증 TTL이 만료됨 | Adobe Primetime 인증 TTL 유효 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple의 장치 토큰 TTL이 만료됨** | 사용자가 인증되지 않음(MVPD 선택기가 나타남) | 사용자가 인증되고 TTL이 Adobe Primetime 인증 토큰의 나머지 시간입니다 |
| **Apple의 장치 토큰 TTL이 유효합니다.** | 사용자는 자동으로 인증되며 TVE 대시보드에 지정된 TTL로 다른 Adobe Primetime 인증 토큰을 가져옵니다 | 사용자가 인증되고 TTL이 Adobe Primetime 인증 토큰의 나머지 시간입니다 |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
