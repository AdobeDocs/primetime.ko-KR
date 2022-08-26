---
title: iOS/tvOS SDK 개요
description: 'iOS/tvOS SDK 개요 '
source-git-commit: 6b9508e56bdaa4876bd0974bf7877fb0c1810919
workflow-type: tm+mt
source-wordcount: '3693'
ht-degree: 0%

---


# iOS/tvOS SDK 개요 {#iostvos-sdk-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.


</br>


## 소개 {#intro}

iOS AccessEnabler는 모바일 앱에서 TV Everywhere의 자격 부여 서비스에 Adobe Primetime 인증을 사용할 수 있도록 해주는 Objective C iOS/tvOS 라이브러리입니다. 구현은 다음과 같이 구성됩니다 *AccessEnabler* 자격 API와 *EntitlementDelegate* 및 *[권한 상태](#ios%20entitlement%20status)* 라이브러리가 트리거하는 콜백을 설명하는 프로토콜입니다. 프로토콜과 함께 인터페이스를 사용하는 경우 다음과 같은 공통 이름이 있습니다. AccessEnabler 라이브러리

## iOS 및 tvOS 요구 사항 {#reqs}

iOS 및 tvOS 플랫폼 및 Primetime 인증과 관련된 최신 기술 요구 사항은 [플랫폼/장치/도구 요구 사항](#ios)를 참조하고 SDK 다운로드에 포함된 릴리스 노트를 참조하십시오. 이 페이지의 나머지 부분에서 특정 SDK 버전 이상에 적용되는 변경 사항을 확인하는 섹션이 보입니다. 예를 들어, 다음은 1.7.5 SDK와 관련된 적절한 노트입니다.

## 기본 클라이언트 워크플로우 이해 {#flows}

기본 클라이언트 워크플로우는 일반적으로 브라우저 기반 Primetime 인증 클라이언트와 동일하거나 매우 유사합니다. 그러나 아래에 설명된 대로 몇 가지 예외가 있습니다.

- [초기화 후 워크플로우](#post-init)
- [일반 초기 인증 워크플로우](#generic)
- [로그아웃 워크플로우](#logout)


### 초기화 후 워크플로우 {#post-init}

AccessEnabler에서 지원하는 모든 자격 부여 워크플로우는 이전에 [`setRequestor()`](#setReq) 자신의 정체성을 확립하기 위해 일반적으로 응용 프로그램의 초기화/설정 단계 동안 한 번만 요청자 ID를 제공하도록 이 호출을 수행합니다.


iOS 기본 클라이언트를 사용, 처음 호출한 후 [`setRequestor()`](#setReq)를 선택하는 경우, 다음 절차를 진행할 수 있습니다.

- 권한 부여 호출을 즉시 시작하고 필요한 경우 해당 호출을 자동으로 큐에 올릴 수 있도록 할 수 있습니다.

- 의 성공/실패에 대한 확인을 받을 수 있습니다 [`setRequestor()`](#setReq) 다음을 수행하여 [`setRequestorComplete()`](#setReqComplete) 콜백입니다.

- 위의 두 가지 작업을 모두 수행할 수 있습니다.

앱이 성공 알림을 받을 때까지 기다리도록 하는 것이 좋습니다 [`setRequestor()`](#setReq) 또는 AccessEnabler의 호출 큐 메커니즘을 사용하도록 합니다. 모든 후속 인증 및 인증 요청에는 요청자 ID와 관련 구성 정보가 필요하므로 [`setRequestor()`](#setReq) 초기화가 완료될 때까지 모든 인증 및 인증 API 호출을 효과적으로 차단합니다.

 

### 일반 초기 인증 워크플로우 {#generic}

이 워크플로우의 목적은 MVPD를 사용하여 사용자에게 로그인하는 것입니다. 성공적으로 로그인하면 백엔드 서버가 사용자에게 인증 토큰을 보냅니다. 인증은 일반적으로 인증 프로세스의 일부로 수행되지만, 다음 단계에서는 인증이 격리 상태에서 작동하는 방법에 대해 설명하고 인증 단계를 포함하지 않습니다.

이 워크플로우는 일반적인 브라우저 기반 인증 워크플로우와 기본 클라이언트에 대해 다르지만 기본 클라이언트와 브라우저 기반 클라이언트 모두에 대해 1-5단계가 동일합니다.

1. 애플리케이션이 AccessEnabler를 호출하여 인증 워크플로우를 시작합니다 `getAuthentication() `유효한 캐시된 인증 토큰을 확인하는 API 메서드.
1. 사용자가 현재 인증되면 AccessEnabler가 [`setAuthenticationStatus()`](#setAuthNStatus) 콜백 함수를 실행하고, 성공을 나타내는 인증 상태를 전달하고, 흐름을 끝냅니다.
1. 사용자가 현재 인증되지 않은 경우 AccessEnabler는 지정된 MVPD에서 사용자의 마지막 인증 시도가 성공했는지 여부를 확인하여 인증 흐름을 계속합니다. MVPD ID가 캐시되고 `canAuthenticate` 플래그가 true이거나 [`setSelectedProvider()`](#setSelProv)로 설정되어 있는 경우 사용자에게 MVPD 선택 대화 상자가 표시되지 않습니다. 인증 흐름은 MVPD의 캐시된 값(즉, 마지막 성공적인 인증 동안 사용된 것과 동일한 MVPD)을 계속 사용합니다. 백엔드 서버에 네트워크 호출이 수행되고 사용자가 MVPD 로그인 페이지로 리디렉션됩니다(아래 6단계).
1. 캐시된 MVPD ID가 없고 [`setSelectedProvider()`](#setSelProv) 또는 `canAuthenticate` 플래그가 false로 설정되어 있고, [`displayProviderDialog()`](#dispProvDialog) 콜백이 호출됩니다. 이 콜백은 사용자가 선택할 MVPD 목록을 표시하는 UI를 애플리케이션에 만들도록 지시합니다. MVPD 선택기를 만드는 데 필요한 정보가 포함된 MVPD 개체 배열이 제공됩니다. 각 MVPD 개체는 MVPD 엔터티에 대해 설명하고 MVPD의 ID(예: XFINITY, AT\&amp;T 등)와 같은 정보를 포함합니다. 및 MVPD 로고가 있는 URL입니다.
1. 특정 MVPD를 선택한 후에는 AccessEnabler에 사용자가 선택한 내용을 알려야 합니다. 사용자가 원하는 MVPD를 선택하면 AccessEnabler에 대한 호출을 통해 사용자 선택을 알려줍니다 [`setSelectedProvider()`](#setSelProv) 메서드를 사용합니다.
1. iOS AccessEnabler가 `navigateToUrl:` callback 또는 `navigateToUrl:useSVC:` 콜백을 사용하여 사용자를 MVPD 로그인 페이지로 리디렉션합니다. AccessEnabler는 두 방법 중 하나를 트리거하여 애플리케이션에 생성 요청을 수행합니다 `UIWebView/WKWebView or SFSafariViewController` 콜백에서 제공된 URL을 로드하기 위해 및 `url` 매개 변수. 백엔드 서버에서 인증 끝점의 URL입니다. tvOS AccessEnabler의 경우 [status()](#status_callback_implementation) 콜백은 `statusDictionary` 매개 변수와 두 번째 화면 인증에 대한 폴링이 즉시 시작됩니다. 다음 `statusDictionary` 다음 포함 `registration code` 두 번째 화면 인증에 사용해야 합니다. 
1. iOS AccessEnabler의 경우 사용자가 MVPD의 로그인 페이지에 도달하여 애플리케이션 매체를 통해 자신의 자격 증명을 입력합니다 `UIWebView/WKWebView or SFSafariViewController `컨트롤러. 이 전송 중에 여러 리디렉션 작업이 발생하고 응용 프로그램이 여러 리디렉션 작업 중에 컨트롤러가 로드한 URL을 모니터링해야 합니다.
1. iOS AccessEnabler의 경우 `UIWebView/WKWebView or SFSafariViewController` 컨트롤러가 응용 프로그램이 컨트롤러를 닫고 AccessEnabler를 호출해야 하는 특정 사용자 지정 URL을 로드합니다. `handleExternalURL:url `API 메서드. 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 인증 흐름이 완료되었으며 을 닫아도 안전하다는 신호로만 응용 프로그램에서 해석해야 합니다 `UIWebView/WKWebView or SFSafariViewController` 컨트롤러. 애플리케이션이 `SFSafariViewController `컨트롤러는 `application's custom scheme` (예: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), 그렇지 않으면 이 특정 사용자 지정 URL이 `ADOBEPASS_REDIRECT_URL` 상수(예: `adobepass://ios.app`).
1. 애플리케이션이 닫히면 `UIWebView/WKWebView or SFSafariViewController` 컨트롤러 및 호출 `handleExternalURL:url `API 메서드에서 AccessEnabler는 백엔드 서버에서 인증 토큰을 검색하고 인증 흐름이 완료되었음을 애플리케이션에 알려줍니다. AccessEnabler가 [`setAuthenticationStatus()`](#setAuthNStatus) 성공을 나타내는 상태 코드가 1인 콜백입니다. 이러한 단계를 실행하는 동안 오류가 발생하면 [`setAuthenticationStatus()`](#setAuthNStatus) 콜백은 인증 실패를 나타내는 상태 코드 및 해당 오류 코드를 사용하여 트리거됩니다.


>[!WARNING]
>
> AccessEnabler가 앱에 대한 제어를 포기하는 단계(예: 공급자 선택 대화 상자가 표시되거나, UIWebView/WKWebView 또는 SFSsafariViewController가 표시되는 경우) 동안 사용자는 인증 흐름을 취소할 수 있습니다. 이러한 경우 앱은 AccessEnabler에 이 이벤트를 알리고 를 호출해야 합니다 [`setSelectedProvider()`](#setSelProv) API 메서드, null을 매개 변수로 전달합니다. 이렇게 하면 AccessEnabler가 내부 상태를 정리하고 인증 흐름을 재설정할 수 있습니다. tvOS에서 동일한 방법을 사용하여 인증 폴링을 취소할 수 있습니다.


### 로그아웃 워크플로우 {#logout}

기본 클라이언트의 경우 로그아웃은 위에서 설명한 인증 프로세스와 유사하게 처리됩니다.

1. 애플리케이션이 AccessEnabler를 호출하여 로그아웃 워크플로우를 시작합니다 `logout() `API 메서드. 로그아웃은 사용자가 Primetime 인증 서버 및 MVPD 서버에서 모두 로그아웃해야 한다는 사실로 인해 일련의 HTTP 리디렉션 작업의 결과입니다. AccessEnabler 라이브러리에서 발행한 간단한 HTTP 요청으로 이 흐름을 완료할 수 없으므로 `UIWebView/WKWebView or SFSafariViewController` HTTP 리디렉션 작업을 따를 수 있으려면 컨트롤러가 인스턴스화되어야 합니다.

1. 인증 흐름과 유사한 패턴이 사용됩니다. iOS AccessEnabler는 `navigateToUrl:` 콜백 또는 `navigateToUrl:useSVC:` 를 만들려면 `UIWebView/WKWebView or SFSafariViewController` 콜백에서 제공된 URL을 로드하기 위해 및 `url` 매개 변수. 백엔드 서버에서 로그아웃 끝점의 URL입니다. tvOS AccessEnabler의 경우 `navigateToUrl:` 콜백 또는 `navigateToUrl:useSVC:` 콜백이 호출됩니다.

1. 여러 리디렉션을 거칠 때 애플리케이션은 `UIWebView/WKWebView or SFSafariViewController `제어하고 특정 사용자 지정 URL을 로드하는 때를 감지합니다. 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 응용 프로그램에서 로그아웃 흐름이 완료되었으며 컨트롤러를 닫아도 안전하다는 신호로만 해석해야 합니다. 컨트롤러가 이 특정 사용자 지정 URL을 로드하면 애플리케이션이 컨트롤러를 닫고 AccessEnabler를 호출해야 합니다 `handleExternalURL:url `API 메서드. 애플리케이션이 `SFSafariViewController `컨트롤러는 `application's custom scheme` (예:`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), 그렇지 않으면 이 특정 사용자 지정 URL이 ` ADOBEPASS_REDIRECT_URL  `상수(예: `adobepass://ios.app`).

1. 마지막으로 AccessEnabler가 [`setAuthenticationStatus()`](#setAuthNStatus) 상태 코드가 0인 콜백으로 로그아웃 흐름의 성공을 나타냅니다.

로그아웃 흐름은 사용자가 `UIWebView/WKWebView or SFSafariViewController`  어떤 식으로든 통제자. 따라서 Adobe은 로그아웃 프로세스 중에 컨트롤을 보이지 않게(즉, 숨김)할 것을 권장합니다.

## 토큰 {#tokens}

- [정의 및 사용](#definitions)
- [캐싱 지침](#caching)
- [지속성](#persistence)
- [형식](#format)
- [장치 바인딩](#device_binding)


### 정의 및 사용 {#definitions}

Primetime 인증 자격 솔루션은 인증 및 인증 워크플로우가 성공적으로 완료될 때 Primetime 인증이 생성하는 특정 데이터(토큰)의 생성을 다룹니다. 이러한 토큰은 클라이언트의 iOS 장치에 로컬로 저장됩니다.

 

토큰은 수명이 제한됩니다. 만료 시 인증 및/또는 인증 워크플로우의 재시작을 통해 토큰을 다시 발급해야 합니다.

 

권한 부여 워크플로우 동안 발행된 토큰은 세 가지 유형이 있습니다.

- **인증 토큰:** 사용자 인증 워크플로우의 최종 결과는 AccessEnabler가 사용자를 대신하여 인증 쿼리를 수행하는 데 사용할 수 있는 인증 GUID입니다. 이 인증 GUID에는 사용자의 인증 세션 자체와 다를 수 있는 연결된 TTL(Time-to-Live) 값이 있습니다. 인증 요청을 시작하는 장치에 인증 GUID를 바인딩하여 인증 토큰이 생성됩니다.
- **인증 토큰:** 고유 resourceID로 식별된 특정 보호된 리소스에 대한 액세스 권한을 부여합니다. 이 ID는 원래 resourceID와 함께 인증 당사자가 발행한 권한 부여로 구성됩니다. 이 정보는 요청을 시작하는 장치에 바인딩됩니다.
- **단기 미디어 토큰:** AccessEnabler는 단기 미디어 토큰을 반환하여 주어진 리소스에 대한 호스팅 애플리케이션에 대한 액세스 권한을 부여합니다. 이 토큰은 해당 특정 리소스에 대해 이전에 획득한 인증 토큰을 기반으로 생성됩니다. 또한 이 토큰이 장치에 바인딩되지 않으며 연결된 수명 범위가 훨씬 짧습니다(기본값: 5분)

인증 및 인증이 성공하면 Primetime 인증은 인증, 인증 및 수명이 짧은 미디어 토큰을 발행합니다. 이러한 토큰은 사용자의 장치에 캐시되고 연관된 수명 동안 사용되어야 합니다.

 

### 캐싱 지침 {#caching}

- 인증 토큰
- 인증 토큰
- 단기 미디어 토큰


#### 인증 토큰

- **AccessEnabler 1.7:** 이 SDK에서는 여러 Programmer-MVPD 버킷을 활성화하여 여러 인증 토큰을 활성화하는 새로운 토큰 저장 방법을 도입했습니다. 이제 동일한 스토리지 레이아웃은 &quot;요청자별 인증&quot; 시나리오 및 일반적인 인증 흐름에 모두 사용됩니다. 두 방법 간의 유일한 차이점은 인증이 수행되는 방식입니다. &quot;요청자별 인증&quot;에는 스토리지(다른 프로그래머용)에 인증 토큰이 존재함에 따라 AccessEnabler가 백 채널 인증을 수행할 수 있는 새로운 개선 사항(수동 인증)이 포함되어 있습니다. 사용자는 한 번만 인증해야 하며 이 세션은 추가 앱에서 인증 토큰을 가져오는 데 사용됩니다. 이 백 채널 플로우는 [`setRequestor()`](#setReq) 은 Programmer에게 거의 투명합니다. **그러나 여기에 하나의 중요한 요구 사항이 있습니다. 프로그래머는 기본 UI 스레드에서 setRequestor()를 호출해야 합니다.**
- **AccessEnabler 1.6 이상:** 장치에서 인증 토큰을 캐시하는 방법은 &quot;**요청자별 인증&quot;** 현재 MVPD와 연결된 플래그:

<!-- end list -->

1. 요청자별 인증 기능이 비활성화되어 있으면 단일 인증 토큰이 글로벌 대지에 로컬로 저장됩니다. 이 토큰은 현재 MVPD와 통합된 모든 응용 프로그램 간에 공유됩니다.
1. 요청자별 인증 기능을 사용하는 경우 토큰이 인증 흐름을 수행한 프로그래머와 명시적으로 연결됩니다(토큰은 글로벌 대지에 저장되지 않고 해당 프로그래머 응용 프로그램에만 표시되는 개인 파일). 특히 서로 다른 응용 프로그램 간의 SSO(Single Sign-On)가 비활성화됩니다. 사용자는 새 앱으로 전환할 때 인증 흐름을 명시적으로 수행해야 합니다(두 번째 앱의 프로그래머가 현재 MVPD와 통합되고 로컬 캐시에 해당 프로그래머에 대한 인증 토큰이 없다는 사실을 제공).

 

#### 인증 토큰

지정한 순간에 AccessEnabler에서 RESOURCE당 하나의 인증 토큰만 캐시됩니다. 캐시된 인증 토큰이 여러 개 있을 수 있지만 서로 다른 리소스와 연결되어 있습니다. 새 인증 토큰이 발급되고 이전 인증 토큰이 이미 있을 때마다 *동일한 리소스*&#x200B;새 토큰은 기존의 캐시된 값을 덮어씁니다.

 

#### 미디어 토큰

단기 미디어 토큰은 캐시하면 안 됩니다. 미디어 토큰은 일회용 사용으로 제한되므로 인증 API가 호출될 때마다 서버에서 검색해야 합니다.

 

### 지속성 {#persistence}

토큰은 동일한 애플리케이션의 연속된 실행에서 지속되어야 합니다. 즉, 인증 및 인증 토큰이 획득되고 사용자가 애플리케이션을 닫으면 사용자가 애플리케이션을 다시 열 때 동일한 토큰을 애플리케이션에서 사용할 수 있습니다. 또한 여러 애플리케이션에서 이러한 토큰을 유지하는 것이 좋습니다. 즉, 사용자가 하나의 애플리케이션을 사용하여 특정 ID 공급자와 로그인(인증 및 인증 토큰을 성공적으로 획득)한 후 다른 애플리케이션을 통해 동일한 토큰을 사용할 수 있으며, 동일한 ID 공급자를 통해 로그인할 때 사용자에게 자격 증명을 묻는 메시지가 더 이상 표시되지 않습니다. 이러한 유형의 원활한 인증/인증 워크플로우가 Primetime 인증 솔루션을 진정한 TV-Every 구현으로 만드는 이유입니다. 

 

## iOS

iOS AccessEnabler 라이브러리는 토큰 데이터를 라는 &quot;클립보드와 유사한&quot; 데이터 구조에 저장하여 애플리케이션 간 데이터 공유의 문제를 해결합니다 *보드 붙여넣기*. 이 시스템 수준 공유 리소스는 원하는 영구 토큰 사용 사례를 구현할 수 있는 주요 요소를 제공합니다.

- **구조화된 스토리지 지원** - 페이스트 보드는 단순한 선형 버퍼와 같은 메모리 구조가 아닙니다. 사용자가 지정한 키 값을 기반으로 데이터 색인화를 허용하는 사전 같은 저장 메커니즘을 제공합니다.
- **기본 파일 시스템을 사용한 데이터 지속성 지원** - 붙여넣기 보드 구조의 내용은 지속으로 표시될 수 있으며, 이때 데이터는 장치의 내부 메모리에 저장된다.

 

특정 토큰을 토큰 캐시에 배치하면 AccessEnabler 라이브러리에서 다른 시간에 해당 유효성을 검사합니다.  유효한 토큰은 다음과 같이 정의됩니다.

- 토큰의 TTL이 만료되지 않았습니다.
- 토큰의 발급자는 허용된 ID 공급자 목록에 포함됩니다.

 

## tvOS

tvOS에서는 임시 보드를 사용할 수 없으므로 tvOS AccessEnabler 라이브러리는 NsUserDefaults를 저장소 옵션으로 사용합니다. 이렇게 하면 인증 및 인증 토큰을 유지하는 문제가 해결되지만 저장된 정보는 다른 애플리케이션 간에 공유할 수 없습니다.

 

**iOS 10 대지 변경 사항 -** 이전 버전의 iOS에서 업그레이드할 때 임시 보드가 지워집니다. 즉, 모든 응용 프로그램을 다시 인증해야 합니다.

 

**iOS 7 대지 변경 사항 -** iOS 7에서 대지가 작동하는 방식의 변경으로 인해 iOS 7에서 실행되는 애플리케이션 간에 제한된 교차 SSO가 있을 것입니다. 동일한 애플리케이션 `<Bundle Seed ID>`( `<Team ID>`)는 토큰을 공유하며, 즉 동일한 프로그래머 X의 앱 A1과 A2가 토큰을 공유하지만 앱 A1(프로그래머 X)과 앱 A3(프로그래머 Y)은 토큰을 공유하지 않습니다. 

- 번들 시드 ID/팀 ID는 동일한 프로비저닝 프로필에 의해 생성된 두 앱 간에 동일합니다. 다음 링크에서 자세한 내용을 확인하십시오.
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- 이 &quot;Cross SSO&quot; 제한은 사용된 Primetime 인증 SDK에 관계없이 iOS 7에 제공됩니다. 

iOS 7 이상(Access Enabler v1.8 이상)에서 SSO 구성에 대한 자세한 내용은 다음 기술 노트를 참조하십시오. <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### 토큰 스토리지(AccessEnabler 1.7)

AccessEnabler 1.7부터 토큰 스토리지는 여러 Programmer-MVPD 조합을 지원할 수 있으며, 여러 인증 토큰을 보유할 수 있는 다중 수준의 중첩 맵 구조에 의존합니다. 이 새 스토리지는 어떤 식으로든 AccessEnabler 공용 API에 영향을 주지 않으며 프로그래머 측에서 변경할 필요가 없습니다. 다음은 이 새로운 기능을 보여주는 예입니다.

1. App1(Programmer1에서 개발)을 엽니다.
1. MVPD1을 인증합니다(Programmer1과 통합).
1. 현재 응용 프로그램을 일시 중단/닫고 App2(Programmer2에서 개발)를 엽니다.
1. Programmer2가 MVPD2와 통합되지 않았다고 가정해 보겠습니다. 따라서 사용자는 App2에서 인증되지 않습니다.
1. App2에서 MVPD2(Programmer2와 통합)로 인증합니다.
1. 다시 App1으로 전환합니다. 사용자는 여전히 Programmer1로 인증됩니다.

이전 버전의 AccessEnabler에서는 토큰 저장소가 이전에 한 개의 인증 토큰만 지원했기 때문에 6단계에서 사용자가 인증되지 않은 것으로 렌더링됩니다.

 

하나의 Programmer / MVPD 세션에서 로그아웃하면 디바이스의 다른 모든 Programmer / MVPD 인증 토큰을 포함하여 전체 기본 저장소가 지워집니다. 반면 인증 흐름을 취소합니다(호출 [`setSelectedProvider(null)`](#setSelProv))은 기본 저장소를 지우지 않지만 현재 Programmer/MVPD 인증 시도(현재 Programmer의 MVPD를 지우는 방법)에만 영향을 줍니다.

 

### 토큰 가져오기(AccessEnabler 1.7)

AccessEnabler 1.7에 포함된 다른 스토리지 관련 기능을 사용하면 이전 스토리지 영역에서 인증 토큰을 가져올 수 있습니다. 이 &quot;토큰 가져오기&quot;를 사용하면 스토리지 버전을 업그레이드할 때에도 SSO 상태를 유지하면서 연속 AccessEnabler 릴리스 간의 호환성을 유지할 수 있습니다. 가져오기 프로그램은 [`setRequestor()`](#setReq) 현재 저장소에 현재 Programmer에 대한 유효한 인증 토큰이 없다고 가정할 경우 다음 두 가지 시나리오에서 흐름 및 실행됩니다.

- 특정 프로그래머가 개발한 1.7 앱의 첫 번째 설치
- 새 스토리지를 사용하는 향후 AccessEnabler로 경로 업그레이드

가져오기 작업은 Programmer에 투명하며 클라이언트 응용 프로그램에서 코드를 변경할 필요가 없습니다.

 

### 토큰 기밀 정보 제거기(AccessEnabler 1.7.5)

AccessEnabler 1.7.5에서 이 서비스는 앞으로 실행됩니다 [`setRequestor()`](#setReq)`. `WiFi MAC 주소에서 추적을 위해 IDFA로 iOS 7 스위치를 전환하여 개발되었습니다. 정리기는 현재 저장소에 유효한 인증 토큰(장치 ID와 관련하여 유효하며, 이전에는 iOS7 이전 MAC 주소를 사용하여 계산되었습니다.). 토큰 기밀 정보 가리기 는 잘못된 모든 토큰을 제거합니다. 

 

AccessEnabler 1.7.5 응용 프로그램을 iOS 6에서 사용한 다음 사용자가 iOS 7으로 업데이트할 때 토큰 기밀 정보 제거기 서비스가 가장 유용합니다. 이렇게 되면 장치 ID 알고리즘이 MAC 주소 사용에서 IDFA로 변경되므로 iOS 6에서 획득한 모든 인증 토큰이 올바르지 않게 됩니다. 잘못된 토큰이 모두 제거되고 사용자가 인증되지 않습니다. 

 

토큰 기밀 정보 제거기가 잘못된 토큰을 제거하지 않으면, 잘못된 인증 토큰이 있으므로 AccessEnabler가 인증을 받지 못합니다. 인증 오류 메시지는 암호화되고 문제의 원인을 파악하는 데 크게 도움이 되지 않으므로 최종 사용자가 디버깅하는 데에는 문제가 있습니다. 

 

### 형식 {#format}

- [AuthN 토큰](#authn_token)
- [AuthZ 토큰](#authz_token)
- [Short Media 토큰](#short_token)
- [장치 바인딩](#device_binding)


AuthN 및 AuthZ 토큰의 형식은 배경 정보에만 여기에 포함됩니다. 이러한 토큰의 구조는 언제든지 Primetime 인증에 의해 변경될 수 있습니다. AuthN 및 AuthZ 토큰은 로컬 장치에 노출되지 않으므로 프로그래머는 앱을 구현하기 위해 AuthN 및 AuthZ 토큰의 정확한 구조를 알지 않아도 됩니다. 짧은 미디어 토큰 *is* Programmer의 애플리케이션에 노출되었습니다.

 

#### 인증 토큰 {#authn_token}

아래 목록은 인증 토큰의 형식을 나타냅니다.

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthenticationToken>
      <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
      <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>   
  </simpleAuthenticationToken>
```
 

#### 인증 토큰 {#authz_token}

아래 목록은 인증 토큰의 형식을 나타냅니다.

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthorizationToken>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
      <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>
  </simpleAuthorizationToken>
```
 

#### Short Media 토큰 {#short_token}

아래 목록은 짧은 미디어 토큰의 형식을 제공합니다. 이 토큰은 Programmer의 응용 프로그램에 노출됩니다. 성공적인 자격 부여 프로세스가 끝나면 Programmer의 애플리케이션에 전달됩니다.

```
  <signatureInfo>signature<signatureInfo>
  <shortAuthorizationToken>
    <sessionGUID>session_guid</sessionGUID>
    <requestorID>requestor_id</requestorID>
    <resourceID>resource_id</resourceID>
    <ttl>ttl_in_ms</ttl>
    <issueTime>issue_time</issueTime>
    <mvpdId>mvpd_id</mvpdId>
    <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
  </shortAuthorizationToken>
```
 

### 장치 바인딩 {#device_binding}

위의 XML 목록에서 태그가 지정된 내용을 확인합니다 `simpleTokenFingerprint`. 이 태그의 목적은 기본 장치 ID 개인화 정보를 보유하는 것입니다. AccessEnabler 라이브러리는 자격 부여 호출 동안 이러한 개인화 정보를 가져와 Primetime 인증 서비스에서 사용할 수 있도록 할 수 있습니다. 서비스는 이 정보를 사용하여 실제 토큰에 포함하므로 토큰을 특정 장치에 효과적으로 결합합니다. 이 방법의 최종 목표는 여러 장치에서 토큰을 전송할 수 없도록 만드는 것입니다.

 

이 기능은 분명히 보안 관련 기능이므로 보안 관점에서 볼 때 이 정보는 기본적으로 &quot;중요&quot;입니다. 따라서, 이러한 정보는 조작 및 도청은 물론 보호되어야 한다. HTTPS 프로토콜을 통해 인증/승인 요청을 보내어 도청문제가 해결됩니다. 위조 방지 장치는 장치 식별 정보에 디지털 서명을 하여 처리됩니다. AccessEnabler 라이브러리는 장치에서 제공한 정보에서 장치 ID를 계산한 다음 장치 ID를 &quot;clear in the Primetime 인증 서버&quot;에 요청 매개 변수로 전송합니다. Primetime 인증 서버는 Adobe의 개인 키로 장치 ID에 디지털 서명을 하고 AccessEnabler로 반환되는 인증 토큰에 추가합니다. 따라서 장치 ID가 인증 토큰과 바인딩된다. 인증 흐름 중에 AccessEnabler는 인증 토큰과 함께 장치 ID를 다시 클리어 보냅니다. 유효성 검사 프로세스가 실패하면 인증/인증 워크플로우가 자동으로 실패합니다. Primetime 인증 서버는 개인 키를 장치 ID에 적용하고 인증 토큰의 값과 비교합니다. 일치하지 않으면 자격 흐름이 실패합니다.

 

**AccessEnabler 1.7.5의 장치 바인딩에 대한 참고 사항:** AccessEnabler 1.7.5부터 장치 ID를 계산하여 iOS 장치에 대한 개인화 정보를 제공하는 방법이 변경되었습니다. 이 변경 사항은 iOS 7의 변경 사항을 반영합니다. iOS 7에서 Apple은 더 이상 IDFA(광고주용 식별자)를 위해 WiFi MAC 주소를 추적 옵션으로 제공하지 않습니다. iOS 7에서 실행되는 앱에 대한 개인화 정보는 IDFA를 기반으로 하며 이 정보가 자격 흐름 토큰에 포함되어 있으므로, 이 변경으로 인해 사용자 환경에 다양한 영향을 줄 수 있습니다. 다양한 효과는 사용자가 업그레이드하고 있는 iOS 버전과 Programmer가 업그레이드하고 있는 AccessEnabler의 버전이 결합되어 있는 경우에 따라 달라집니다. 이 변경에 대한 자세한 내용은 AccessEnabler SDK 1.7.5에 포함된 릴리스 노트를 참조하십시오.


## 관련 정보 {#related}

<!--
- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
