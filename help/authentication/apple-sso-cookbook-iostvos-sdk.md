---
title: Apple SSO Cookbook(iOS/tvOS SDK)
description: Apple SSO Cookbook(iOS/tvOS SDK)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---



# Apple SSO Cookbook(iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#Introduction}

Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK는 Apple SSO 워크플로우를 통해 iOS, iPadOS 또는 tvOS에서 실행되는 클라이언트 애플리케이션의 최종 사용자를 위해 플랫폼 SSO(Single Sign-On) 인증을 지원할 수 있습니다.

이 문서는 기존 AccessEnabler iOS/tvOS SDK 설명서에 대한 확장 기능 역할을 하며 다음 문서를 찾을 수 있습니다 [여기](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## 요리책 {#Cookbook}

Apple SSO 사용 환경을 활용하려면 AccessEnabler iOS/tvOS SDK를 통합하여 아래 표시된 팁 시퀀스를 따라야 합니다.

</br>

### 전제 조건 {#Prerequisites}

</br>

#### 권한

>[!TIP]
>
> **<u>Pro 팁:</u>** 사용자의 구독 정보에 액세스하려면 사용자가 장치의 카메라 또는 마이크에 대한 액세스를 제공하는 것과 같이 계속 진행할 수 있도록 애플리케이션 권한을 부여해야 합니다. 응용 프로그램별로 이 권한을 요청해야 하며 장치가 사용자의 선택을 저장합니다. 사용자는 애플리케이션 설정(TV 공급자 권한 액세스)이나 *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* tvOS에서

>[!TIP]
>
> **<u>Pro 팁:</u>** 애플리케이션이 전경 상태가 되면 사용자의 권한을 요청하는 것이 좋지만, 애플리케이션이 확인할 수 있으므로 이것은 제안일 뿐입니다 [액세스 권한](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 사용자 인증을 요구하기 전에 언제든지 사용자의 구독 정보를 볼 수 있습니다. 또한 AccessEnabler iOS/tvOS SDK API는 필요할 때 사용자 권한을 자동으로 요청합니다.

>[!TIP]
>
> **<u>Pro 팁:</u>** 사용자가 가입 정보에 대한 액세스 권한을 부여하지 않거나 비디오 가입자 계정 프레임워크와의 통신이 실패하는 경우 AccessEnabler iOS/tvOS SDK는 일반 인증 플로우로 폴백됩니다.

>[!TIP]
>
> **<u>Pro 팁:</u>** SSO(Single Sign-On) 사용자 환경의 이점을 설명하여 구독 정보에 액세스할 수 있는 권한을 부여하지 않는 사용자에게 인센티브를 제공하는 것이 좋습니다. 사용자는 애플리케이션 설정(TV 공급자 권한 액세스)이나 *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* tvOS에서


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

</br>

#### 콜백

>[!TIP]
>
> **<u>Pro 팁:</u>** 다음 목록을 구현합니다 [콜백](/help/authentication/iostvos-sdk-api-reference.md) Apple SSO 워크플로우에만 해당됩니다.

- [*presentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) - Apple MVPD 선택기가 열릴 때 트리거되는 콜백입니다.
- [*discloseTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) - Apple MVPD 선택기를 닫을 때 트리거되는 콜백입니다.

</br>

#### 오류 보고

>[!TIP]
>
> **<u>Pro 팁:</u>** 다음 목록을 구현합니다 [고급 오류 코드](/help/authentication/error-reporting.md) Apple SSO 워크플로우에만 해당됩니다.

- ***N003*** - 사용자가 Apple MVPD 선택기에서 &quot;기타 TV 공급자&quot; 옵션을 선택했습니다.
- ***N004*** - 사용자가 현재 요청자에 의해 지원되지 않는(통합 또는 Single Sign-On 비활성화됨) Apple MVPD 선택기에서 TV 공급자를 선택했습니다.
- ***N005*** - 사용자가 일반 MVPD 선택기나 Apple MVPD 선택기를 취소하기로 결정했습니다.
- ***VSA403*** - 사용자의 TV 공급자 권한이 응용 프로그램에 대해 거부되었습니다.
- ***VSA404*** - 사용자의 TV 공급자 권한이 응용 프로그램에 대해 확인되지 않았습니다.
- ***VSA503*** - 비디오 가입자 계정 메타데이터 요청이 실패했습니다. 추가 컨텍스트가 *메시지* 필드.
- ***AAPL / APPL_ERROR*** - 비디오 가입자 계정 메타데이터 요청이 실패했습니다. 추가 컨텍스트가 *세부 정보* 필드. 

</br>

### 인증 {#Authentication}

>[!TIP]
>
> **<u>팁:</u>** iOS/iPadOS/tvOS 구현에 대해서는 아래 절차를 따르십시오.

1. 신청서는 [초기화](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) AccessEnabler iOS/tvOS SDK입니다.
1. 신청서는 [현재 요청자 식별자 설정](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **중요 사항:** 이 두 번째 단계는 [고급 오류 코드](/help/authentication/error-reporting.md) Apple SSO 워크플로우에만 적용됩니다 **다음 중 한 가지는 true입니다**:

   - ***VSA403*** - 사용자의 TV 공급자 권한이 응용 프로그램에 대해 거부되었습니다.
   - ***VSA404*** - 사용자의 TV 공급자 권한이 응용 프로그램에 대해 확인되지 않았습니다.
   - ***APPL*** - AccessEnabler iOS/tvOS SDK와 비디오 가입자 계정 프레임워크 간의 통신에 오류가 발생했습니다.

   이 두 번째 단계는 경우에 따라 Adobe 인증 토큰에 대해 Apple SSO 프로필을 자동으로 교환하려고 합니다 **위의 모든 것은 false입니다** 및 **다음은 모두 사실이다**:

   - 응용 프로그램에 대한 사용자의 TV 공급자 권한이 부여됩니다.
   - 사용자가 장치 시스템 수준에서 TV 공급자 계정에 로그인됩니다.
   - AccessEnabler iOS/tvOS SDK는 비디오 가입자 계정 프레임워크에서 사용자의 TV 공급자 식별자를 수신했습니다.
   - Adobe Primetime TVE 대시보드를 통해 사용자의 애플리케이션과의 TV Provider 통합을 사용할 수 있습니다.
   - 애플리케이션을 사용하는 사용자의 TV 공급자 Single Sign-On은 Adobe Primetime TVE 대시보드를 통해 활성화됩니다.
   - Adobe Primetime TVE Dashboard를 통해 사용자의 TV 공급자가 저하되지 않습니다.
   - AccessEnabler iOS/tvOS SDK는 비디오 가입자 계정 프레임워크에서 사용자의 TV 공급자 SAML 응답을 수신했습니다.

   **<u>Pro 팁:</u>** 이 두 번째 단계는 [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) 콜백으로, 애플리케이션에서 인증을 명시적으로 시작하지 않았으므로

1. 신청서는 [인증 상태 확인](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **중요 사항:** 이 세 번째 단계는 [고급 오류 코드](/help/authentication/error-reporting.md) Apple SSO 워크플로우에만 적용됩니다 **다음 중 한 가지는 true입니다**:

   - ***VSA403** - 사용자가 장치 시스템 수준에서 TV 공급자 계정에 로그인되었지만 사용자의 TV 공급자 권한이 응용 프로그램에 대해 거부됩니다.
   - ***VSA404** - 사용자가 장치 시스템 수준에서 TV 공급자 계정에 로그인되었지만 사용자의 TV 공급자 권한이 해당 응용 프로그램에 대해 확인되지 않았습니다.
   - ***APPL\_ERROR** - 사용자가 장치 시스템 수준에서 TV Provider 계정에 로그인했지만 AccessEnabler iOS/tvOS SDK와 비디오 가입자 계정 프레임워크 간의 통신에서 오류가 발생했습니다.

   **중요 사항:** 이 세 번째 단계는 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 콜백 *상태* 이면 0과 같음 **다음 중 한 가지는 true입니다**:

   - 사용자는 장치 시스템 수준 또는 일반 인증 흐름을 통해 TV 공급자 계정에 로그인하지 않습니다.
   - 사용자가 장치 시스템 수준 또는 일반 인증 흐름을 통해 TV Provider 계정에 로그인했지만 사용자의 TV Provider 인증 토큰 TTL이 전달되었습니다.
   - 사용자가 장치 시스템 수준에서 또는 일반 인증 흐름을 통해 TV Provider 계정에 로그인했지만 Adobe Primetime TVE Dashboard를 통해 사용자의 TV Provider 통합에 사용할 수 없습니다.
   - 사용자가 장치 시스템 수준에서 TV Provider 계정에 로그인했지만 Adobe Primetime TVE Dashboard를 통해 애플리케이션을 사용하는 사용자의 TV Provider Single Sign-On이 비활성화됩니다.
   - 사용자가 장치 시스템 수준에서 TV 공급자 계정에 로그인되었지만 사용자의 TV 공급자 권한이 응용 프로그램에 대해 거부됩니다.
   - 사용자가 장치 시스템 수준에서 TV 공급자 계정에 로그인되어 있지만 사용자의 TV 공급자 권한은 응용 프로그램에 대해 확인되지 않습니다.
   - 사용자가 장치 시스템 수준에서 TV Provider 계정에 로그인했지만 AccessEnabler iOS/tvOS SDK와 비디오 가입자 계정 프레임워크 간의 통신에 오류가 발생했습니다.

   **중요 사항:** 이 세 번째 단계는 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 콜백 *상태* 의 경우 1과 같음 **위의 모든 것은 false입니다.**


1. 신청서는 [인증 초기화](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) 이전 인증 상태 검사가 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 콜백 *상태* 0과 같습니다.

   **<u>Pro 팁:</u>** 다음 AccessEnabler iOS/tvOS SDK API 중 하나를 구현합니다 [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) 또는 [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **중요 사항:** 이 네 번째 단계는 [고급 오류 코드](/help/authentication/error-reporting.md) Apple SSO 워크플로우에만 적용됩니다 **다음 중 한 가지는 true입니다**:

   - ***VSA403*** - 사용자의 TV 공급자 권한이 응용 프로그램에 대해 거부되었습니다.
   - ***VSA404*** - 사용자의 TV 공급자 권한이 응용 프로그램에 대해 확인되지 않았습니다.
   - ***VSA503*** - AccessEnabler iOS/tvOS SDK와 비디오 가입자 계정 프레임워크 간의 통신에 오류가 발생했습니다.
   - ***N003*** - 사용자가 Apple MVPD 선택기에서 &quot;기타 TV 공급자&quot; 옵션을 선택했습니다.
   - ***N004*** - 사용자가 현재 요청자에 의해 지원되지 않는(통합 또는 Single Sign-On 비활성화됨) Apple MVPD 선택기에서 TV 공급자를 선택했습니다.
   - ***N005*** - 사용자가 일반 MVPD 선택기나 Apple MVPD 선택기를 취소하기로 결정했습니다.

   **중요 사항:** 이 네 번째 단계는 를 트리거하여 일반 인증 흐름에 대체됩니다 [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) callback 및 **하나** 위의 [고급 오류 코드](/help/authentication/error-reporting.md)인 경우 **위 중 하나가 사실이다**. 

   **중요 사항:** 이 네 번째 단계는 를 트리거하여 일반 인증 흐름에 대체됩니다 [navigateToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) 또는 [navigateToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) callback 및 **없음** 위의 [고급 오류 코드](/help/authentication/error-reporting.md): 사용자가 Apple SSO를 지원하지 않지만 Apple MVPD 선택기에 있는 TV 공급자를 선택한 경우

   **<u>Pro 팁:</u>** AccessEnabler iOS/tvOS SDK는 자동으로 [setSelectedProvider](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API: 사용자가 Apple SSO를 지원하지 않지만 Apple MVPD 선택기에 있는 TV 공급자를 선택한 경우

   **중요 사항:** 이 네 번째 단계는 경우에 따라 Apple SSO 프로필을 Adobe 인증 토큰으로 자동 교환하려고 합니다 **위의 모든 것은 false입니다** 및 **다음은 모두 사실이다**:

   - 응용 프로그램에 대한 사용자의 TV 공급자 권한이 부여됩니다.
   - 사용자가 로그인한 경우/현재 장치 시스템 수준에서 TV 공급자 계정에 로그인되어 있습니다.
   - AccessEnabler iOS/tvOS SDK는 비디오 가입자 계정 프레임워크에서 사용자의 TV 공급자 식별자를 수신했습니다.
   - Adobe Primetime TVE 대시보드를 통해 사용자의 애플리케이션과의 TV Provider 통합을 사용할 수 있습니다.
   - 애플리케이션을 사용하는 사용자의 TV 공급자 Single Sign-On은 Adobe Primetime TVE 대시보드를 통해 활성화됩니다.
   - Adobe Primetime TVE Dashboard를 통해 사용자의 TV 공급자가 저하되지 않습니다.
   - AccessEnabler iOS/tvOS SDK는 비디오 가입자 계정 프레임워크에서 사용자의 TV 공급자 SAML 응답을 수신했습니다.


 

>**<u>Pro 팁:</u>** 이 네 번째 단계는 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) 콜백의 *상태* 따라서 응용 프로그램에서 인증을 명시적으로 시작했기 때문에


</br>

### 메타데이터 {#Metadata}

애플리케이션에는 플랫폼 SSO를 통해 로그인한 결과로 인증이 발생했는지 여부를 확인하는 선택 사항이 있습니다. &quot;*tokenSource&quot;* [사용자 메타데이터](/help/authentication/iostvos-sdk-api-reference.md#getMeta) AccessEnabler iOS/tvOS SDK의 API입니다.

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### 로그아웃 {#Logout}

다음 [비디오 가입자 계정](https://developer.apple.com/documentation/videosubscriberaccount) 프레임워크는 장치 시스템 수준에서 TV 공급자 계정에 로그인한 사용자를 프로그래밍 방식으로 로그아웃하는 API를 제공하지 않습니다. 따라서 로그아웃을 완전히 적용하려면 최종 사용자가 명시적으로 *`Settings -> TV Provider`* iOS/iPadOS에서 또는 *`Settings -> Accounts -> TV Provider`* tvOS에서 사용자가 가질 다른 옵션은 특정 애플리케이션 설정 섹션(TV 공급자 권한 액세스)에서 사용자의 구독 정보에 액세스할 권한을 철회하는 것입니다.

>[!TIP]
>
> **<u>팁:</u>** AccessEnabler iOS/tvOS SDK 매체를 통해 이를 구현합니다 [로그아웃](/help/authentication/iostvos-sdk-api-reference.md#logout) API.


>[!TIP]
>
> **<u>Pro 팁:</u>** tvOS 구현에 대해서는 아래 절차를 따르십시오.

- 신청서는 [로그아웃 시작](/help/authentication/iostvos-sdk-api-reference.md#logout) AccessEnabler iOS/tvOS SDK에서 지원됩니다. 이렇게 하면 MVPD 측에서 세션 정리를 쉽게 할 수 없습니다.
- 애플리케이션이 사용자에게 명시적으로 로그아웃하도록 지시하거나 메시지를 표시해야 합니다. *`Settings -> Accounts -> TV Provider`* tvOS에서만 [*VSA203* 상태 코드가 트리거됨](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>Pro 팁:</u>** iOS/iPadOS 구현에 대해서는 아래 절차를 따르십시오.

- 신청서는 [로그아웃 시작](/help/authentication/iostvos-sdk-api-reference.md#logout) AccessEnabler iOS/tvOS SDK에서 지원됩니다. 이렇게 하면 MVPD 측에서 세션 정리를 용이하게 할 수 있습니다.
- 애플리케이션이 사용자에게 명시적으로 로그아웃하도록 지시하거나 메시지를 표시해야 합니다. *`Settings -> TV Provider`* iOS/iPadOS의 경우 [*VSA203* 상태 코드가 트리거됨](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
