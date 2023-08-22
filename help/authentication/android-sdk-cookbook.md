---
title: Android SDK Cookbook
description: Android SDK Cookbook
exl-id: 7f66ab92-f52c-4dae-8016-c93464dd5254
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# Android SDK Cookbook {#android-sdk-cookbook}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

</br>

## 소개 {#intro}

이 문서에서는 Android AccessEnabler 라이브러리에서 공개한 API를 통해 프로그래머 상위 수준 애플리케이션이 구현할 수 있는 자격 부여 워크플로에 대해 설명합니다.


Android용 Adobe Primetime 인증 자격 솔루션은 궁극적으로 두 개의 도메인으로 나뉩니다.

- UI 도메인 - UI를 구현하고 AccessEnabler 라이브러리에서 제공하는 서비스를 사용하여 제한된 콘텐츠에 액세스할 수 있는 상위 레벨 애플리케이션 계층입니다.
- AccessEnabler 도메인 - 권한 부여 워크플로우는 다음과 같은 형태로 구현됩니다.
   - Adobe의 백엔드 서버에 대한 네트워크 호출
   - 인증 및 권한 부여 워크플로와 관련된 비즈니스 논리 규칙
   - 다양한 리소스 관리 및 워크플로 상태 처리(예: 토큰 캐시)

AccessEnabler 도메인의 목적은 권한 부여 워크플로의 모든 복잡성을 숨기고 AccessEnabler 라이브러리를 통해 권한 부여 워크플로를 구현하는 간단한 권한 부여 기본 세트를 상위 레이어 애플리케이션에 제공하는 것입니다.

1. 요청자 ID 설정
1. 특정 ID 공급자에 대한 인증 확인 및 가져오기
1. 특정 리소스에 대한 권한 부여 확인 및 받기
1. 로그아웃

AccessEnabler의 네트워크 작업은 다른 스레드에서 수행되므로 UI 스레드가 차단되지 않습니다. 따라서 두 애플리케이션 도메인 간의 양방향 통신 채널은 완전히 비동기적인 패턴을 따라야 합니다.

- UI 애플리케이션 레이어는 AccessEnabler 라이브러리에 의해 노출된 API 호출을 통해 AccessEnabler 도메인에 메시지를 전송합니다.
- AccessEnabler는 UI 레이어가 AccessEnabler 라이브러리에 등록하는 AccessEnabler 프로토콜에 포함된 콜백 메서드를 통해 UI 레이어에 응답합니다.

## 권한 흐름 {#entitlement}

1. [전제 조건](#prereqs)
1. [시작 흐름](#startup_flow)
1. [인증 흐름](#authn_flow)
1. [인증 흐름](#authz_flow)
1. [미디어 흐름 보기](#media_flow)
1. [로그아웃 흐름](#logout_flow)



### A. 사전 요구 사항 {#prereqs}

1. 콜백 함수를 만듭니다.
   - [`setRequestorComplete()`](#$setRequestorComplete)

     트리거 기준 `setRequestor()`는 성공 또는 실패를 반환합니다.\
     성공 은 권한 부여 호출을 계속할 수 있음을 나타냅니다.

   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

     트리거 기준 `getAuthentication()` 사용자가 공급자(MVPD)를 선택하지 않고 아직 인증되지 않은 경우에만 해당합니다.\
     다음 `mvpds` 매개 변수는 사용자가 사용할 수 있는 공급자의 배열입니다.

   - [`setAuthenticationStatus(status, errorcode)`](#$setAuthNStatus)

     트리거 기준 `checkAuthentication()` 항상.\
     트리거 기준 `getAuthentication()` 사용자가 이미 인증되고 공급자를 선택한 경우에만 해당합니다.

     반환된 상태는 성공 또는 실패이며, errorcode는 실패 유형을 설명합니다.

   - [navigateToUrl(url)](#$navigateToUrl)

     트리거 기준 `getAuthentication()` 사용자가 MVPD를 선택하면 다음 `url` 매개 변수는 MVPD의 로그인 페이지 위치를 제공합니다.

   - [`sendTrackingData(event, data)`](#$sendTrackingData)

     트리거 기준 `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.\
     다음 `event` 매개 변수는 발생한 권한 부여 이벤트를 나타냅니다. `data` 매개 변수는 이벤트와 관련된 값의 목록입니다.

   - [`setToken(token, resource)`](#$setToken)

     트리거 기준 `checkAuthorization()` 및 `getAuthorization()` 리소스를 볼 수 있는 인증 성공 후.\
     다음 `token` 매개 변수는 단기 미디어 토큰입니다. `resource` 매개 변수는 사용자에게 보기 권한이 있는 콘텐츠입니다.

   - [`tokenRequestFailed(resource, code, description)`](#$tokenRequestFailed)

     트리거 기준 `checkAuthorization()` 및 `getAuthorization()` 인증에 실패한 후.\
     다음 `resource` 매개 변수는 사용자가 보려고 한 콘텐츠입니다. `code` parameter는 발생한 실패 유형을 나타내는 오류 코드입니다. `description` 매개 변수는 오류 코드와 관련된 오류를 설명합니다.

   - [`selectedProvider(mvpd)`](#$selectedProvider)

     트리거 기준 `getSelectedProvider()`.\
     다음 `mvpd` 매개 변수는 사용자가 선택한 공급자에 대한 정보를 제공합니다.

   - [&#39;setMetadataStatus(메타데이터, 키, 인수)&#39;](#$setMetadataStatus)

     트리거 기준 `getMetadata().`\
     다음 `metadata` 매개 변수는 요청한 특정 데이터를 제공합니다. `key` 매개 변수는 `getMetadata()` 요청 및 `arguments` 매개 변수가에 전달된 것과 동일한 사전입니다. `getMetadata()`.

   - [&#39;preauthorizedResources(resources)&#39;](#$preauthResources)

     트리거 기준 `checkPreauthorizedResources()`.\
     다음 `authorizedResources` 매개 변수는 사용자에게 보기 권한이 있는 리소스를 제공합니다.


![](assets/android-entitlement-flows.png)


### B. 시작 흐름 {#startup_flow}

1. 상위 수준 응용 프로그램을 시작합니다.
1. Adobe Primetime 인증 시작

   a. 호출 [`getInstance`](#$getInstance) Adobe Primetime 인증 AccessEnabler의 단일 인스턴스를 만듭니다.

   - **종속성:** Adobe Primetime 인증 기본 Android 라이브러리(AccessEnabler)

   b. 호출` setRequestor()` 프로그래머의 신원을 확인하다. `requestorID` 및 (선택 사항) Adobe Primetime 인증 엔드포인트 배열.

   - **종속성:** 유효한 Adobe Primetime 인증 요청자 ID\
     (Adobe Primetime 인증 계정 관리자와 협력하여 이를 정리하십시오.)

   - **트리거:** setRequestorComplete() callback

   | 참고 |     |
   | --- | --- |  
   | ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/icons/1313859077_lightbulb.png) | 요청자 ID가 완전히 설정될 때까지 권한 부여 요청을 완료할 수 없습니다. 이는 setRequestor()가 계속 실행 중인 동안 모든 후속 권한 요청(예: `checkAuthentication()`)은 차단됩니다.<br><br>두 가지 구현 옵션이 있습니다. 요청자 식별 정보가 백엔드 서버로 전송되면 UI 애플리케이션 레이어가 다음 두 가지 접근 방식 중 하나를 선택할 수 있습니다.<br><br>1.  의 트리거를 기다립니다. `setRequestorComplete()` callback(AccessEnabler 대리자의 일부).  이 옵션은 다음과 같은 가장 확실성을 제공합니다. `setRequestor()` 완료되었으므로 대부분의 구현에 권장됩니다.<br>2.  이 트리거될 때까지 기다리지 않고 계속합니다. `setRequestorComplete()` 콜백을 실행하고 권한 부여 요청 실행을 시작합니다. 이러한 호출(checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout)은 AccessEnabler 라이브러리에 의해 큐에 추가되며 이후에 실제 네트워크 호출을 수행합니다. `setRequestor(). `네트워크 연결이 불안정한 경우 이 옵션이 중단되는 경우가 있습니다. |

1. 호출 [checkAuthentication()](#$checkAuthN) 전체 인증 흐름을 시작하지 않고 기존 인증을 확인합니다.   이 호출이 성공하면 인증 플로우로 직접 진행할 수 있습니다.  그렇지 않으면 인증 플로우로 이동합니다.

   - **종속성:** 에 대한 성공적인 호출 `setRequestor()` (이 종속성은 모든 후속 호출에도 적용됩니다.)

   - **트리거:** setAuthenticationStatus() callback



### C. 인증 흐름 {#authn_flow}

1. 호출 [`getAuthentication()`](#$getAuthN) 인증 흐름을 시작하거나 사용자가 이미 인증되었다는 확인을 받습니다.\
   **트리거:**
   - 사용자가 이미 인증된 경우 setAuthenticationStatus() 콜백입니다.  이 경우 로 직접 이동합니다. [인증 흐름](#authz_flow).
   - 사용자가 아직 인증되지 않은 경우 displayProviderDialog() 콜백입니다.

1. (으)로 전송된 공급자 목록이 있는 사용자 표시 `displayProviderDialog()`.

1. 사용자가 공급자를 선택한 후, 사용자로부터 사용자 MVPD의 URL을 가져옵니다. `navigateToUrl()` callback.  WebView를 열고 해당 WebView 컨트롤을 URL로 보냅니다.

1. 이전 단계에서 인스턴스화된 WebView를 통해 사용자는 MVPD의 로그인 페이지에 도달하고 로그인 자격 증명을 입력합니다. WebView 내에서 여러 리디렉션 작업이 수행됩니다.


   **참고:** 이 시점에서 사용자는 인증 흐름을 취소할 수 있습니다. 이 경우 UI 레이어는 를 호출하여 이 이벤트에 대해 AccessEnabler에 알립니다. `setSelectedProvider()` 포함 `null` 를 매개 변수로 사용하십시오. 이렇게 하면 AccessEnabler가 내부 상태를 정리하고 인증 흐름을 재설정할 수 있습니다.

1. 사용자가 성공적으로 로그인하면 애플리케이션 레이어가 &quot;사용자 지정 리디렉션 URL&quot;(즉,: [http://adobepass.android.app](http://adobepass.android.app/)). 이 사용자 지정 URL은 실제로 WebView에서 로드하기 위한 것이 아닌 잘못된 URL입니다. 인증 흐름이 완료되었으며 WebView를 닫아야 한다는 신호입니다.

1. WebView 컨트롤을 닫고 `getAuthenticationToken()`: AccessEnabler가 백엔드 서버에서 인증 토큰을 검색하도록 지시합니다.

1. [선택 사항] 호출 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 을 눌러 사용자가 볼 수 있는 권한이 있는 리소스를 확인합니다. 다음 `resources` 매개 변수는 사용자의 인증 토큰과 연결된 보호된 리소스의 배열입니다.\
   **트리거:** `preAuthorizedResources()` callback\
   **실행 지점:** 완료된 인증 흐름 이후

1. 인증이 성공하면 인증 플로우로 진행합니다.



### D. 인증 흐름 {#authz_flow}

1. 호출 [getAuthorization()](#$getAuthZ) 인증 흐름을 시작합니다.

   종속성: 유효한 ResourceID가 MVPD와(과) 합의되었습니다.

   **참고:** ResourceID는 다른 장치 또는 플랫폼에서 사용되는 ID와 동일해야 하며 MVPD에서 동일합니다.

1. 인증 및 권한 부여의 유효성을 검사합니다.

   - 다음과 같은 경우 `getAuthorization()` 호출 성공: 사용자에게 유효한 AuthN 및 AuthZ 토큰이 있습니다(사용자는 요청된 미디어를 시청하도록 인증되고 승인됨).
   - If `getAuthorization()` 실패: throw된 예외를 검사하여 해당 유형(AuthN, AuthZ 또는 그 외 다른 것)을 확인합니다.
      - 인증(AuthN) 오류인 경우 인증 흐름을 다시 시작합니다.
      - 인증(AuthZ) 오류인 경우 사용자에게 요청된 미디어를 볼 수 있는 권한이 없으며 사용자에게 일종의 오류 메시지가 표시되어야 합니다.
      - 다른 유형의 오류(연결 오류, 네트워크 오류 등)가 있는 경우 그런 다음 사용자에게 적절한 오류 메시지를 표시합니다.

1. 짧은 미디어 토큰의 유효성을 검사합니다.\
   Adobe Primetime 인증 미디어 토큰 검증기 라이브러리를 사용하여 다음에서 반환된 단기 미디어 토큰을 확인합니다. `getAuthorization()` 위의 호출:

   - 유효성 검사가 성공하는 경우: 사용자에 대해 요청된 미디어를 재생합니다.
   - 유효성 검사에 실패하는 경우: AuthZ 토큰이 잘못되었으며 미디어 요청이 거부되고 오류 메시지가 사용자에게 표시되어야 합니다.

1. 일반 애플리케이션 플로우로 돌아갑니다.

### E. 미디어 흐름 보기 {#media_flow}

1. 사용자가 보려는 미디어를 선택합니다.
2. 미디어는 보호됩니까?  응용 프로그램에서 선택한 미디어가 보호되어 있는지 확인합니다.
- 선택한 미디어가 보호되면 애플리케이션이 [인증 흐름](#authz_flow) 위.
- 선택한 미디어가 보호되지 않으면 사용자를 위해 미디어를 재생합니다.



### F. 로그아웃 흐름 {#logout_flow}

1. 호출 [`logout()`](#$logout) 로그아웃할 수 있습니다.\
   AccessEnabler는 현재 요청자와 SSO(Single Sign-On)가 있는 요청자에 대해 현재 MVPD에 대해 캐시된 모든 값과 토큰을 지웁니다. 캐시를 지운 후 AccessEnabler가 서버 호출을 수행하여 서버측 세션을 정리합니다.  서버 호출로 인해 IdP로 SAML 리디렉션이 발생할 수 있으므로(IdP측에서 세션 정리가 허용됨) 이 호출은 모든 리디렉션을 따라야 합니다. 따라서 이 호출은 WebView 컨트롤 내에서 처리되어야 합니다.

   a. 인증 워크플로와 동일한 패턴에 따라 AccessEnabler 도메인은 다음을 통해 UI 애플리케이션 계층에 요청을 수행합니다.`navigateToUrl()` callback)을 사용하여 WebView 컨트롤을 만들고 해당 컨트롤이 백엔드 서버에 로그아웃 끝점의 URL을 로드하도록 지시합니다.

   b. UI는 WebView 컨트롤의 활동을 모니터링하고 컨트롤이 여러 리디렉션을 거치면서 애플리케이션의 사용자 지정 URL(예: [http://adobepass.android.app/](http://adobepass.android.app/)). 이 이벤트가 발생하면 UI 애플리케이션 레이어가 WebView를 닫고 로그아웃 프로세스가 완료됩니다.

   **참고:** 로그아웃 흐름은 사용자가 어떤 방식으로든 WebView와 상호 작용할 필요가 없다는 점에서 인증 흐름과 다릅니다. UI 애플리케이션 레이어는 WebView 를 사용하여 모든 리디렉션이 준수되는지 확인합니다. 따라서 로그아웃 프로세스 중에 WebView 컨트롤을 보이지 않게(즉, 숨김으로) 만들 수 있습니다(권장).



### 여러 MVPD 및 로그아웃을 사용한 로그인을 위한 사용자 흐름 {#user_flows}

[여기](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AndroidSSOUserFlows.pdf) 여러 MVPD를 사용할 때의 동작과 사용자가 애플리케이션에서 로그아웃할 때 발생하는 상황을 설명하는 문서가 있습니다.

설명된 동작은 Android SDK 버전 >= 2.0.0을 사용할 때 사용할 수 있습니다.
