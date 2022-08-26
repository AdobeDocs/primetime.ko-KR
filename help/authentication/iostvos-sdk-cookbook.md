---
title: iOS/tvOS Cookbook
description: iOS/tvOS Cookbook
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '2434'
ht-degree: 0%

---


# iOS/tvOS SDK Cookbook {#iostvos-sdk-cookbook}

- [소개](#intro)
- [자격 흐름](#entitlement)
- [관련 정보](#related)

>[!NOTE]
>
>**알림**: 이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>


## 소개 {#intro}

이 문서에서는 iOS/tvOS AccessEnabler 라이브러리에 의해 노출된 API를 통해 Programmer의 상위 수준 애플리케이션에서 구현할 수 있는 자격 부여 워크플로우를 설명합니다.

 

iOS/tvOS용 Adobe Primetime 인증 자격 솔루션은 궁극적으로 두 도메인으로 분할됩니다.

- UI 도메인 - UI를 구현하고 AccessEnabler 라이브러리에서 제공하는 서비스를 사용하여 제한된 컨텐츠에 액세스할 수 있는 상위 수준 애플리케이션 계층입니다.
- AccessEnabler 도메인 - 자격 부여 워크플로우가 다음 형태로 구현되는 곳입니다.
   - Adobe의 백엔드 서버에 대한 네트워크 호출
   - 인증 및 인증 워크플로우와 관련된 비즈니스 논리 규칙
   - 다양한 리소스 관리 및 워크플로우 상태(예: 토큰 캐시) 처리

AccessEnabler 도메인의 목표는 자격 부여 워크플로우의 모든 복잡한 내용을 숨기고 권한 부여 워크플로우를 구현하는 간단한 권한 프리미티브 집합을 상위 계층 응용 프로그램(AccessEnabler 라이브러리를 통해)에 제공하는 것입니다.

1. 요청자 ID 설정
1. 특정 ID 공급자에 대한 인증 확인 및 가져오기
1. 특정 리소스에 대한 권한을 확인하고 가져옵니다.
1. 로그아웃
1. Apple VSA 프레임워크를 프록시하여 Apple SSO 흐름

AccessEnabler의 네트워크 작업은 자체 스레드에서 발생하므로 UI 스레드는 차단되지 않습니다. 따라서 두 애플리케이션 도메인 간의 양방향 통신 채널은 완전히 비동기적인 패턴을 따라야 합니다.

- UI 애플리케이션 계층은 AccessEnabler 라이브러리에 의해 노출된 API 호출을 통해 AccessEnabler 도메인에 메시지를 보냅니다.
- AccessEnabler는 UI 계층이 AccessEnabler 라이브러리에 등록하는 AccessEnabler 프로토콜에 포함된 콜백 메서드를 통해 UI 레이어에 응답합니다.

 

## 방문자 ID 구성 {#visitorIDSetup}

구성 [Marketing Cloud visitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) analytics POV에서는 값이 매우 중요합니다. visitorID 값이 설정되면 SDK는 모든 네트워크 호출과 함께 이 정보를 전송하고 Adobe Primetime 인증 서버에서 이 정보를 수집합니다. 향후에는 Adobe Primetime 인증 서비스의 분석과 다른 애플리케이션 또는 웹 사이트에서 보유할 수 있는 다른 분석 보고서와 관련 지을 수 있습니다. visitorID 설정 방법에 대한 정보를 찾을 수 있습니다 [여기](#setOptions).

 

## 자격 흐름 {#entitlement}

A.  [전제 조건](#prereqs) </br>
B.  [시작 흐름](#startup_flow) </br>
C.  [Apple SSO 내의 인증 흐름](#authn_flow_wo_applesso)  </br>
D.  [iOS에서 Apple SSO를 사용한 인증 흐름](#authn_flow_with_applesso) </br>
E.  [tvOS에서 Apple SSO를 사용한 인증 흐름](#authn_flow_with_applesso_tvOS) </br>
F.  [인증 흐름](#authz_flow) </br>
G.  [미디어 흐름 보기](#media_flow) </br>
H.  [Apple SSO를 사용하지 않고 로그아웃 흐름](#logout_flow_wo_AppleSSO) </br>
나.  [Apple SSO를 사용한 로그아웃 흐름](#logout_flow_with_AppleSSO) </br>

 

### A. 사전 요구 사항 {#prereqs}

1. 콜백 함수를 만듭니다.
   - `setRequestorComplete()` </br>
      - 트리거된 사람 [setRequestor()](#$setReq)성공 또는 실패를 반환합니다. </br>
      - 성공 은 자격 호출을 계속 진행할 수 있음을 나타냅니다.
   - [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      - 트리거된 사람 [`getAuthentication()`](#$getAuthN) 사용자가 공급자(MVPD)를 선택하지 않았고 아직 인증되지 않은 경우에만 해당합니다. </br>
      - 다음 `mvpds` 매개 변수는 사용자가 사용할 수 있는 공급자 배열입니다.
   - `setAuthenticationStatus(status, errorcode)` </br>
      - 트리거된 사람 `checkAuthentication()` 항상  </br>
      - 트리거된 사람 [`getAuthentication()`](#$getAuthN) 사용자가 이미 인증되고 공급자를 선택한 경우에만 해당됩니다. </br>
      - 반환된 상태는 성공 또는 실패이며 오류 코드는 실패 유형을 설명합니다.
   - [`navigateToUrl(url)`](#$nav2url) </br>
      - 트리거된 사람 [`getAuthentication()`](#$getAuthN) 사용자가 MVPD를 선택하면  다음 `url` 매개 변수는 MVPD의 로그인 페이지 위치를 제공합니다.
   - `sendTrackingData(event, data)` </br>
      - 트리거된 사람 `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.
      - 다음 `event` 매개 변수는 자격 이벤트가 발생한 경우를 나타냅니다. a `data` 매개 변수는 이벤트와 관련된 값 목록입니다. 
   - `setToken(token, resource)`

      - 트리거된 사람 [checkAuthorization()](#checkAuthZ) 및 [getAuthorization()](#$getAuthZ) 리소스를 볼 수 있는 권한이 성공적으로 부여된 후.
      - 다음 `token` 매개 변수는 단기 미디어 토큰입니다. a `resource` 매개 변수는 사용자가 볼 수 있는 권한이 있는 콘텐츠입니다.
   - `tokenRequestFailed(resource, code, description)` </br>
      - 트리거된 사람 [checkAuthorization()](#checkAuthZ) 및 [getAuthorization()](#$getAuthZ) 승인 실패 후.
      - 다음 `resource` 매개 변수는 사용자가 보려고 하는 콘텐츠입니다. a `code` 매개 변수는 발생한 실패 유형을 나타내는 오류 코드입니다. a `description` 매개 변수는 오류 코드와 연관된 오류를 설명합니다.
   - `selectedProvider(mvpd)` </br>
      - 트리거된 사람 [`getSelectedProvider()`](#getSelProv).
      - 다음 `mvpd` 매개 변수는 사용자가 선택한 공급자에 대한 정보를 제공합니다.
   - `setMetadataStatus(metadata, key, arguments)`
      - 트리거된 사람 `getMetadata().`
      - 다음 `metadata` 매개 변수는 요청한 특정 데이터를 제공합니다. a
         `key` 매개 변수는 [getMetadata()](#getMeta)
요청; 그리고 
`arguments` 매개 변수는 에 전달된 것과 동일한 사전입니다 [getMetadata()](#getMeta).
   - [&#39;preauthorizedResources(authorizedResources)&#39;](#preauthResources)

      - 트리거된 사람 [`checkPreauthorizedResources()`](#checkPreauth).
      - 다음 `authorizedResources` 매개 변수는 사용자가 볼 수 있는 권한이 있는 리소스를 나타냅니다.
   - [&#39;presentTvProviderDialog(viewController)&#39;](#presentTvDialog)
      - 트리거된 사람 [getAuthentication()](#getAuthN) 현재 요청자가 SSO 지원이 있는 MVPD에서 적어도 하나를 지원하는 경우
      - viewController 매개 변수는 Apple SSO 대화 상자이며 기본 보기 컨트롤러에 표시되어야 합니다.
   - [&#39;disffTvProviderDialog(viewController)&#39;](#dismissTvDialog)
      - Apple SSO 대화 상자에서 &quot;취소&quot; 또는 &quot;기타 TV 공급자&quot;를 선택하여 사용자 작업에 의해 트리거됩니다.
      - viewController 매개 변수는 Apple SSO 대화 상자이며 기본 보기 컨트롤러에서 해제해야 합니다.












</br>


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOS_flows\(1\).png)\
 

### B. 시작 흐름 {#startup_flow}

1. 상위 수준 응용 프로그램을 시작합니다.</br>
1. Adobe Primetime 인증 시작 </br></br>
a. 호출 [`init`](#$init) Adobe Primetime 인증 AccessEnabler의 단일 인스턴스를 생성하려면
   - **종속성:** Adobe Primetime 인증 기본 iOS/tvOS 라이브러리(AccessEnabler)
   나. 호출 `setRequestor()` 프로그래머의 정체성을 확립하기 위해서 프로그래머에게 `requestorID` 및(선택 사항) Adobe Primetime 인증 엔드포인트의 배열입니다. tvOS의 경우 공개 키와 암호를 제공해야 합니다. 자세한 내용은 [Clientless 설명서](#create_dev) 자세한 내용
   - **종속성:** 유효한 Adobe Primetime 인증 RequestorID\
      (Adobe Primetime 인증 계정 관리자와 함께 이를 정렬합니다.)
   - **트리거:**

      [setRequestorComplete()](#$setReqComplete) callback
   >[!NOTE]
   >
   > **참고:** 요청자 ID가 완전히 설정될 때까지 자격 요청을 완료할 수 없습니다. 이것은 [`setRequestor()`](#$setReq)  가 계속 실행 중이면 이후의 모든 자격 요청(예: [`checkAuthentication()`](#checkAuthN) 차단되었습니다.

   다음 두 가지 구현 옵션이 있습니다. 요청자 식별 정보가 백엔드 서버로 전송되면 UI 애플리케이션 계층은 다음 두 가지 방법 중 하나를 선택할 수 있습니다. </br>
   1. 의 트리거링을 기다립니다. [`setRequestorComplete()`](#setReqComplete) 콜백(AccessEnabler 위임의 일부)  이 옵션은 [`setRequestor()`](#$setReq) 완료되었으므로 대부분의 구현에 권장됩니다.
   1. 트리거할 때까지 기다리지 않고 계속 진행합니다 [`setRequestorComplete()`](#setReqComplete) 콜백하고 권한 요청 실행을 시작합니다. 이러한 호출(checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout)은 AccessEnabler 라이브러리에서 큐에 대기 중입니다. 이 라이브러리는 [`setRequestor()`](#$setReq). 예를 들어 네트워크 연결이 불안정할 경우 이 옵션이 가끔 중단될 수 있습니다.



1. 호출 `checkAuthentication()` 전체 인증 흐름을 시작하지 않고 기존 인증을 확인합니다.  이 호출이 성공하면 인증 흐름을 직접 진행할 수 있습니다.  없는 경우 인증 플로우로 진행합니다.

   - **종속성:** 에 대한 성공적인 호출 [setRequestor()](#$setReq)
(이 종속성은 모든 후속 호출에도 적용됩니다.)

   - **트리거:** [setAuthenticationStatus()](#$setAuthNStatus) callback

 

### C. Apple SSO를 사용하지 않는 인증 흐름 {#authn_flow_wo_applesso}

1. 호출 [`getAuthentication()`](#$getAuthN) 인증 흐름을 시작하거나 사용자가 이미 인증되었음을 확인합니다. \
   **트리거:**  

   - 다음 [setAuthenticationStatus()](#$setAuthNStatus) 콜백으로 설정되어야 합니다.  이 경우 로 바로 이동합니다 [인증 흐름](#authz_flow).
   - 다음 [displayProviderDialog()](#$dispProvDialog) 콜백으로 설정되어야 합니다.  

1. 사용자에게 전송된 공급자 목록을 제공합니다.
   [`displayProviderDialog()`](#dispProvDialog).

1. 사용자가 공급자를 선택하면, `navigateToUrl:` 또는 `navigateToUrl:useSVC:` 콜백 및 열기 `UIWebView/WKWebView` 또는 `SFSafariViewController` 컨트롤러를 사용하여 해당 컨트롤러를 URL로 연결합니다.   

1. 사용 `UIWebView/WKWebView` 또는 `SFSafariViewController` 이전 단계에서 인스턴스화하면 사용자가 MVPD의 로그인 페이지에 도달하여 로그인 자격 증명을 입력합니다. 컨트롤러 내에서 여러 리디렉션 작업이 발생합니다.</br></br>
   **참고** - 이 시점에서 사용자는 인증 흐름을 취소할 수 있습니다. 이러한 경우 UI 레이어는 AccessEnabler에 이 이벤트를 알리기 위해 [setSelectedProvider()](#setSelProv) with `null` 매개 변수로 사용됩니다. 이렇게 하면 AccessEnabler가 내부 상태를 정리하고 인증 흐름을 재설정할 수 있습니다.

1. 사용자가 성공적으로 로그인하면 애플리케이션 레이어에서 특정 사용자 지정 URL의 로드를 감지합니다. 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 인증 흐름이 완료되었으며 을 닫아도 안전하다는 신호로만 응용 프로그램에서 해석해야 합니다 `UIWebView/WKWebView` 또는 `SFSafariViewController` 컨트롤러. 경우에 따라 `SFSafariViewController `컨트롤러가 특정 사용자 지정 URL을 **`application's custom scheme`** (예:`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), 그렇지 않으면 이 특정 사용자 지정 URL이 **`ADOBEPASS_REDIRECT_URL`** 상수(예: `adobepass://ios.app`).

1. UIWebView/WKWebView 또는 SFSsafariViewController를 닫고 AccessEnabler를 호출합니다 `handleExternalURL:url `API 메서드`,` AccessEnabler가 백엔드 서버에서 인증 토큰을 검색하도록 지시합니다. 

1. [선택 사항입니다] 호출    [`checkPreauthorizedResources(resources)`](#$checkPreauth) 확인할 수 있는 리소스를 확인합니다.  다음 `resources` 매개 변수는 사용자의 인증 토큰과 연결된 보호된 리소스의 배열입니다.  사용자의 MVPD에서 획득한 인증 정보를 사용하는 한 가지 방법은 UI를 장식하는 것입니다(예: 보호된 콘텐츠 옆에 잠금/잠금 해제된 기호).

   - **트리거:** [`preauthorizedResources()`](#preauthResources) callback
   - **실행 지점:** 완료된 인증 흐름 후

1. 인증이 성공하면 인증 흐름을 진행합니다.

 

### iOS에서 Apple SSO를 사용한 인증 흐름 {#authn_flow_with_applesso}

1. 호출 [`getAuthentication()`](#$getAuthN) 인증 흐름을 시작하거나 사용자가 이미 인증되었음을 확인합니다. \
   **트리거:**  

   - 다음 [presentTvProviderDialog()](#presentTvDialog) callback, 사용자가 인증되지 않고 현재 요청자가 SSO를 지원하는 MVPD에 대해 적어도 한 개 이상 있는 경우. MVPD가 SSO를 지원하지 않으면 클래식 인증 흐름이 사용됩니다.

1. 사용자가 공급자를 선택하면 AccessEnabler 라이브러리는 Apple의 VSA 프레임워크에서 제공하는 정보를 사용하여 인증 토큰을 얻습니다.

1. 다음 [setAuthenticationStatus()](#setAuthNStatus) 콜백이 트리거됩니다. 이때 사용자는 Apple SSO로 인증되어야 합니다.

1. [선택 사항입니다] 호출 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 확인할 수 있는 리소스를 확인합니다. 다음 `resources` 매개 변수는 사용자의 인증 토큰과 연결된 보호된 리소스의 배열입니다.  사용자의 MVPD에서 획득한 인증 정보를 사용하는 한 가지 방법은 UI를 장식하는 것입니다(예: 보호된 콘텐츠 옆에 잠금/잠금 해제된 기호).

   - **트리거:** [`preauthorizedResources()`](#preauthResources) callback
   - **실행 지점:** 완료된 인증 흐름 후

1. 인증이 성공하면 인증 흐름을 진행합니다.

 

### tvOS에서 Apple SSO를 사용한 인증 흐름 {#authn_flow_with_applesso_tvOS}

1. 호출 [`getAuthentication()`](#$getAuthN) 인증 흐름을 시작하거나 사용자가 이미 인증되었음을 확인합니다. \
   **트리거:**  
   - 다음 [`presentTvProviderDialog()`](#presentTvDialog) callback, 사용자가 인증되지 않고 현재 요청자가 SSO를 지원하는 MVPD에 대해 적어도 한 개 이상 있는 경우. MVPD가 SSO를 지원하지 않으면 클래식 인증 흐름이 사용됩니다.

1. 사용자가 공급자를 선택한 후 [`status()`](#status_callback_implementation) 콜백이 호출됩니다. 등록 코드가 제공되며 AccessEnabler 라이브러리가 성공적인 두 번째 화면 인증을 위해 서버에 폴링을 시작합니다.

1. 제공된 등록 코드를 사용하여 두 번째 화면에서 인증한 경우 [`setAuthenticatiosStatus()`](#setAuthNStatus) 콜백이 트리거됩니다. 이때 사용자는 Apple SSO로 인증되어야 합니다.
1. [선택 사항입니다] 호출 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 확인할 수 있는 리소스를 확인합니다. 다음 `resources` 매개 변수는 사용자의 인증 토큰과 연결된 보호된 리소스의 배열입니다.  사용자의 MVPD에서 획득한 인증 정보를 사용하는 한 가지 방법은 UI를 장식하는 것입니다(예: 보호된 콘텐츠 옆에 잠금/잠금 해제된 기호).
   - **트리거:** [`preauthorizedResources()`](#preauthResources) callback
   - **실행 지점:** 완료된 인증 흐름 후
1. 인증이 성공하면 인증 흐름을 진행합니다.

 

### F. 인증 흐름 {#authz_flow}

1. 호출 [getAuthorization()](#$getAuthZ) 인증 흐름을 시작합니다.
   - **종속성:** 유효한 ResourceID가 MVPD와 동의됩니다.
   - 리소스 ID는 다른 장치 또는 플랫폼에서 사용되는 ID와 동일해야 하며 MVPD에서 동일합니다. 리소스 ID에 대한 자세한 내용은 [보호된 리소스 식별](https://tve.helpdocsonline.com/4-2-2-3)

1. 인증 및 권한 부여의 유효성을 검사합니다.

   - 만약 [getAuthorization()](#$getAuthZ) 호출 성공: 사용자에게 유효한 AuthN 및 AuthZ 토큰이 있습니다(사용자가 인증되고 요청된 미디어를 볼 수 있는 권한이 있음).
   - If [getAuthorization()](#$getAuthZ) 실패: throw된 예외를 검사하여 해당 유형(AuthN, AuthZ 등)을 확인합니다.
      - 인증(AuthN) 오류인 경우 인증 흐름을 다시 시작합니다.
      - 인증(AuthZ) 오류인 경우 사용자는 요청된 미디어를 볼 수 있는 권한이 없으며 일부 오류 메시지가 사용자에게 표시되어야 합니다.
      - 다른 유형의 오류(연결 오류, 네트워크 오류 등)가 있는 경우 그런 다음 사용자에게 적절한 오류 메시지를 표시합니다.

1. 짧은 미디어 토큰의 유효성을 검사합니다.\
   Adobe Primetime 인증 미디어 토큰 확인 프로그램 라이브러리를 사용하여 [getAuthorization()](#$getAuthZ) 위에 호출하십시오.

   - 유효성 검사가 성공하면: 사용자에 대해 요청된 미디어를 재생합니다.
   - 유효성 검사가 실패한 경우: AuthZ 토큰이 잘못되었습니다. 미디어 요청이 거부되어야 하며 오류 메시지가 사용자에게 표시되어야 합니다.


1. 일반 응용 프로그램 흐름으로 돌아갑니다.

 

### G. 미디어 흐름 보기 {#media_flow}

1. 사용자가 볼 미디어를 선택합니다.
1. 미디어가 보호됩니까?  선택한 미디어가 보호되어 있는지 애플리케이션에서 확인합니다.
   - 선택한 미디어를 보호하면 애플리케이션이 [인증 흐름](#authz_flow) 위에 표시됩니다.
   - 선택한 미디어가 보호되지 않은 경우 사용자를 위해 미디어를 재생합니다.

 

### H. Apple SSO 없이 로그아웃 흐름 {#logout_flow_wo_AppleSSO}

1. 호출 [`logout()`](#$logout) 를 입력하여 사용자를 로그아웃합니다. AccessEnabler는 캐시된 모든 값과 토큰을 지웁니다. 캐시를 지운 후 AccessEnabler는 서버 호출을 수행하여 서버측 세션을 정리합니다. 서버 호출로 인해 IdP로 SAML 리디렉션이 발생할 수 있으므로(IdP 측에서 세션 정리를 허용) 이 호출은 모든 리디렉션을 따라야 합니다. 이러한 이유로 이 호출은 UIWebView/WKWebView 또는 SFSsafariViewController 내에서 처리되어야 합니다.

   - a. 인증 워크플로우와 동일한 패턴을 따라 AccessEnabler 도메인은 를 통해 UI 애플리케이션 레이어에 요청을 수행합니다 `navigateToUrl:` 또는 `navigateToUrl:useSVC:` 콜백을 수행하려면 UIWebView/WKWebView 또는 SFSsafariViewController를 만들고 콜백에서 제공하는 URL을 로드하도록 지시하십시오 `url` 매개 변수. 백엔드 서버에서 로그아웃 끝점의 URL입니다.

   - 나. 애플리케이션이 `UIWebView/WKWebView or SFSafariViewController` 컨트롤러는 몇 개의 리디렉션을 통과하므로 특정 사용자 지정 URL을 로드할 시점을 감지합니다. 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 응용 프로그램에서 로그아웃 플로우가 완료되었으며 을 닫아도 안전하다는 신호로만 해석해야 합니다 `UIWebView/WKWebView` 또는 `SFSafariViewController` 컨트롤러. 컨트롤러가 이 특정 사용자 지정 URL을 로드하면 애플리케이션이 `UIWebView/WKWebView or SFSafariViewController` 컨트롤러 및 AccessEnabler 호출 `handleExternalURL:url`API 메서드. 경우에 따라 `SFSafariViewController`컨트롤러가 특정 사용자 지정 URL을 **`application's custom scheme`** (예: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), 그렇지 않으면 이 특정 사용자 지정 URL이 **`ADOBEPASS_REDIRECT_URL`**  상수(예: `adobepass://ios.app`).

      >[!NOTE]
      >
      > **참고:** 로그아웃 흐름은 사용자가 어떤 식으로든 UIWebView/WKWebView 또는 SFSsafariViewController와 상호 작용할 필요가 없다는 점에서 인증 흐름과 다릅니다. UI 응용 프로그램 계층은 UIWebView/WKWebView 또는 SFSsafariViewController를 사용하여 모든 리디렉션이 수행되는지 확인합니다. 따라서 로그아웃 프로세스 중에 컨트롤러가 보이지 않도록(즉, 숨김) 할 수 있습니다.


### I. Apple SSO에서 로그아웃 흐름 {#logout_flow_with_AppleSSO}

1. 호출 [`logout()`](#$logout) 를 입력하여 사용자를 로그아웃합니다. 
1. 다음 [status()](#status_callback_implementation) 콜백은 id VSA203을 사용하여 호출됩니다.
1. 사용자는 시스템 설정에서도 로그인해야 합니다. 따라서 응용 프로그램을 다시 시작할 때 재인증이 발생합니다.

</br>

### 관련 정보 {#related}

<!---
- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note) ](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->
