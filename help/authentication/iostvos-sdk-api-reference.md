---
title: iOS/tvOS API 참조
description: iOS/tvOS API 참조
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '7000'
ht-degree: 0%

---


# iOS/tvOS SDK API 참조 {#iostvos-sdk-api-reference}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개 {#intro}

이 페이지에서는 Adobe Primetime 인증을 위해 iOS/tvOS 기본 클라이언트가 노출하는 방법 및 콜백 함수에 대해 설명합니다. 여기에 설명된 메서드 및 콜백 함수는 `AccessEnabler.h` 및 `EntitlementDelegate.h` 헤더 파일; iOS AccessEnabler SDK에서 찾을 수 있는 위치는 다음과 같습니다. `[SDK directory]/AccessEnabler/headers/api/`


관련 설명서:

* 기본 Primetime 인증 자격 흐름에 대한 설명은 다음을 참조하십시오 [자격 흐름](/help/authentication/entitlement-flow.md).
* 이 API를 사용하여 Primetime 인증 자격 흐름을 구현하는 방법에 대한 단계별 설명은 [iOS 통합 Cookbook](/help/authentication/iostvos-sdk-cookbook.md).
* 최신 iOS AccessEnabler SDK에 대해서는 다음을 참조하십시오 [iOS Native Access Enabler 라이브러리](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

>[!NOTE]
>
>Adobe은 Primetime 인증만 사용하도록 권장합니다 *공용* API:
>
>* 공개 API는 지원되는 모든 클라이언트 유형에서 사용 및 완전히 테스트됩니다. 모든 공개 기능에 대해 각 클라이언트 유형에 관련 메서드 버전이 있는지 확인합니다.
>* 이전 버전과의 호환성을 지원하고 파트너 통합이 중단되지 않도록 하려면 공개 API가 가능한 한 안정적이어야 합니다. 그러나 비공개 API의 경우 Adobe는 향후 언제든지 서명을 변경할 수 있는 권한을 갖습니다. 현재 공개 Primetime 인증 API 호출의 조합을 통해 지원할 수 없는 특정 흐름이 발생하면 알려 주는 것이 가장 좋습니다. 여러분의 요구 사항을 고려하여, Adobe에서는 공개 API를 수정하고 안정적인 솔루션을 제공할 수 있습니다.


</br>

## API 참조 {#apis}

* [init](#initWithSoftwareStatement):softwareStatement - AccessEnabler 개체를 인스턴스화합니다.

* **[사용되지 않음]** [init](#init) - AccessEnabler 개체를 인스턴스화합니다.

* [setOptions:options:](#setOptions) - 프로필 또는 visitorID와 같은 글로벌 SDK 옵션을 구성합니다.

* [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:serviceProviders:](#setReqV3) - 프로그래머의 ID를 설정합니다.

* **[사용되지 않음]** [setRequestor:signedRequestorId:](#setReq),[setRequestor:signedRequestorId:serviceProviders:](#setReq) - 프로그래머의 ID를 설정합니다.

* **[사용되지 않음]** [setRequestor:signedRequestorId:secret:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos)프로그래머의 정체성을 확립합니다.

* [setRequestorComplete:](#setReqComplete) - 구성 단계가 완료되었음을 애플리케이션에 알립니다.

* [checkAuthentication](#checkAuthN) - 현재 사용자의 인증 상태를 확인합니다.

* [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN) - 전체 인증 워크플로우를 시작합니다.

* [getAuthentication:filter](#getAuthN_filter),[getAuthentication:withData:](#getAuthN)[andFilter](#getAuthN_filter) - 전체 인증 워크플로우를 시작합니다.

* [displayProviderDialog:](#dispProvDialog) - 사용자가 MVPD를 선택할 수 있도록 애플리케이션에 적절한 UI 요소를 인스턴스화하도록 알려줍니다.

* [setSelectedProvider:](#setSelProv) - 사용자의 MVPD 선택을 AccessEnabler에 알려줍니다.

* [navigateToUrl:](#nav2url) - 사용자에게 MVPD 로그인 페이지를 제공해야 한다고 애플리케이션에 알립니다.

* [navigateToUrl:useSVC:](#nav2urlSVC) - SFSsafariViewController를 사용하여 사용자에게 MVPD 로그인 페이지를 제공해야 한다고 애플리케이션에 알립니다.

* [handleExternalURL:url](#handleExternalURL) - 인증/로그아웃 흐름을 완료합니다.

* **[사용되지 않음]** [getAuthenticationToken](#getAuthNToken) - 백 엔드 서버에서 인증 토큰을 요청합니다.

* [setAuthenticationStatus:errorCode:](#setAuthNStatus) - 응용 프로그램에 인증 흐름의 상태를 알려줍니다.

* [checkPreauthorizedResources:](#checkPreauth) - 사용자가 이미 특정 보호된 리소스를 볼 수 있는 권한이 있는지 확인합니다.

* [checkPreauthorizedResources:cache:](#checkPreauthCache) - 사용자가 이미 특정 보호된 리소스를 볼 수 있는 권한이 있는지 확인합니다.

* [preauthorizedResources:](#preauthResources) - 사용자가 이미 볼 수 있는 권한이 있는 리소스 목록을 제공합니다.

* [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ) - 현재 사용자의 인증 상태를 확인합니다.

* [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ) - 인증 흐름을 시작합니다.

* [setToken:forResource:](#setToken) - 인증 흐름이 성공적으로 완료되었음을 애플리케이션에 알립니다.

* [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) - 인증 흐름이 실패했음을 애플리케이션에 알립니다.

* [로그아웃](#logout) - 로그아웃 흐름을 시작합니다.

* [getSelectedProvider](#getSelProv) - 현재 선택한 공급자를 결정합니다.

* [selectedProvider:](#selProv) - 현재 선택된 MVPD에 대한 정보를 애플리케이션에 전달합니다.

* [getMetadata:](#getMeta) - AccessEnabler 라이브러리에서 메타데이터로 노출된 정보를 검색합니다.

* [presentTvProviderDialog:](#presentTvDialog) - 애플리케이션에 Apple SSO 대화 상자를 표시하도록 알려줍니다.

* [discardTvProviderDialog:](#dismissTvDialog) - Apple SSO 대화 상자를 숨기도록 애플리케이션에 알립니다.

* [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus) - 에서 요청한 메타데이터를 전달합니다. [getMetadata:](#getMeta) 호출.

* [sendTrackingData:forEventType:](#sendTracking) - 추적 데이터 정보를 전달합니다.

* [MVPD](#mvpd) - MVPD 클래스입니다. [MVPD에 대한 정보를 포함합니다]

### init:softwareStatement {#initWithSoftwareStatement}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** AccessEnabler 개체를 인스턴스화합니다. 애플리케이션 인스턴스마다 AccessEnabler 인스턴스가 하나씩 있어야 합니다.

| **API 호출: iOS AccessEnabler 생성자** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**사용 가능:** v3.0+

**매개 변수:**

* **softwareStatement:** Adobe 시스템에서 애플리케이션을 식별하는 문자열입니다. 소프트웨어 구문을 얻는 방법을 확인하십시오.

[맨 위로..](#apis)



### init - [사용되지 않음]{#init}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** AccessEnabler 개체를 인스턴스화합니다. 애플리케이션 인스턴스마다 AccessEnabler 인스턴스가 하나씩 있어야 합니다.

| API 호출: iOS AccessEnabler 생성자 |
| --- |
| ```- (id) init;``` |

**사용 가능:** v1.0+ **까지:** v3.0

**매개 변수:** 없음

[맨 위로..](#apis)

</br>

### setOptions:options {#setOptions}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 글로벌 SDK 옵션을 구성합니다. NSDictionary를 인수로 허용합니다. 사전의 값은 SDK에서 수행하는 모든 네트워크 호출과 함께 서버에 전달됩니다.

**참고:** 값은 현재 흐름(인증/인증)과 관계없이 서버에 전달됩니다. 값을 변경하려는 경우 언제든지 이 메서드를 호출할 수 있습니다.

| API 호출: setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**사용 가능:** v2.3.0+

**매개 변수:**

* *옵션*: 글로벌 SDK 옵션이 포함된 NSDictionary입니다. 현재 다음 옵션을 사용할 수 있습니다.
   * **applicationProfile** - 이 값을 기반으로 서버 구성을 만드는 데 사용할 수 있습니다.
   * **visitorID** - Marketing Cloud visitorID. 이 값은 나중에 고급 분석 보고서에 사용할 수 있습니다.
   * **handleSVC** - 프로그래머가 SFSsafariViewController를 처리할지 여부를 나타내는 부울 값 자세한 내용은 [iOS SDK 3.2 이상에서 SFSsafariViewController 지원](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) 자세한 내용
      * 로 설정된 경우 **false,** sdk는 최종 사용자에게 SFSsafariViewController를 자동으로 제공합니다. SDK가 MVPD 로그인 페이지 URL로 더 이동합니다.
      * 로 설정된 경우 **true,** SDK가 **NOT** 최종 사용자에게 SFSsafariViewController를 자동으로 표시합니다. SDK가 더 트리거됩니다 **navigate(toUrl:{url}, useSVC:YES)**.
* **device\_info** - 에 설명된 대로 클라이언트 정보 [클라이언트 정보 전달](/help/authentication/passing-client-information-device-connection-and-application.md).

[맨 위로..](#apis)


### setRequestor:requestorID, setRequestor:requestorID:serviceProviders: {#setReqV3}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 프로그래머의 ID를 설정합니다. Primetime 인증 시스템의 Adobe에 등록하면 각 프로그래머에게 고유 ID가 할당됩니다. SSO 및 원격 토큰을 처리할 때 응용 프로그램이 백그라운드에 있을 때 인증 상태를 변경할 수 있으며, 시스템 상태와 동기화하기 위해 응용 프로그램을 포그라운드로 가져올 때 setRequestor를 다시 호출할 수 있습니다(SSO가 활성화된 경우 원격 토큰 가져오기 또는 그 동안 로그아웃이 발생한 경우 로컬 토큰을 삭제).

서버 응답에는 MVPD 목록과 함께 Programmer의 ID에 첨부된 일부 구성 정보가 포함되어 있습니다. 서버 응답은 AccessEnabler 코드에서 내부적으로 사용됩니다. 작업 상태(즉, 성공/실패)만 를 통해 애플리케이션에 표시됩니다 `setRequestorComplete:` 콜백입니다.

만약 `urls` 매개 변수가 사용되지 않으면 결과 네트워크 호출은 기본 서비스 공급자 URL을 타겟으로 합니다. Adobe 릴리스/프로덕션 환경입니다.


에 값이 제공된 경우 `urls` 매개 변수, 결과 네트워크 호출은 `urls` 매개 변수. 모든 구성 요청은 별도의 스레드에서 동시에 트리거됩니다. MVPD 목록을 컴파일할 때 첫 번째 응답기가 우선합니다. 목록에 있는 각 MVPD에 대해 AccessEnabler는 연관된 서비스 공급자의 URL을 기억합니다. 이후의 모든 자격 요청은 구성 단계 동안 대상 MVPD와 연결된 서비스 공급자와 연결된 URL로 전달됩니다.

| API 호출: 요청자 구성 |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**사용 가능:** v3.0+

| API 호출: 요청자 구성 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**사용 가능:** v3.0+

**매개 변수:**

* *requestorID*: 프로그래머와 연결된 고유 ID입니다. Primetime 인증 서비스에 처음 등록할 때 Adobe에서 할당한 고유 ID를 사이트에 전달합니다.
* *url*: 선택적 매개 변수; 기본적으로 Adobe 서비스 공급자가 사용됩니다(http://sp.auth.adobe.com/). 이 배열을 사용하면 Adobe에서 제공하는 인증 및 인증 서비스의 끝점을 지정할 수 있습니다(다른 인스턴스는 디버깅 목적으로 사용될 수 있음). 이를 사용하여 여러 Primetime 인증 서비스 공급자 인스턴스를 지정할 수 있습니다. 이때 MVPD 목록은 모든 서비스 공급자의 끝점으로 구성됩니다. 각 MVPD는 가장 빠른 서비스 공급자와 연결됩니다. 즉, 먼저 응답하고 해당 MVPD를 지원하는 공급자입니다.

>[!NOTE]
>
>호출 없이 `serviceProviders` 매개 변수를 사용하면 라이브러리가 기본 서비스 공급자(즉, `https://sp.auth.adobe.com` 프로덕션 프로파일 또는 `https://sp.auth-staging.adobe.com` 용). 만약 `serviceProviders` 매개 변수가 제공되면 URL의 배열이어야 합니다. 지정한 모든 끝점에서 구성 정보를 검색하고 병합됩니다. 서로 다른 서비스 공급자 응답에 중복 정보가 있는 경우 가장 빠른 응답 서버(즉, 가장 짧은 응답 시간이 있는 서버가 우선함)를 위해 충돌이 해결됩니다.

**콜백이 트리거됨:** [`setRequestorComplete:`](#setReqComplete)

[맨 위로..](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:serviceProviders: - [사용되지 않음] {#setReq}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 프로그래머의 ID를 설정합니다. Primetime 인증 시스템의 Adobe에 등록하면 각 프로그래머에게 고유 ID가 할당됩니다. SSO 및 원격 토큰을 처리할 때 응용 프로그램이 백그라운드에 있을 때 인증 상태를 변경할 수 있습니다. 시스템 상태와 동기화하기 위해 응용 프로그램을 포그라운드로 가져올 때 setRequestor를 다시 호출할 수 있습니다(SSO가 활성화된 경우 원격 토큰을 가져오거나 그 동안 로그아웃이 발생한 경우 로컬 토큰을 삭제).

서버 응답에는 MVPD 목록과 함께 Programmer의 ID에 첨부된 일부 구성 정보가 포함되어 있습니다. 서버 응답은 AccessEnabler 코드에서 내부적으로 사용됩니다. 작업 상태(즉, 성공/실패)만 를 통해 애플리케이션에 표시됩니다 `setRequestorComplete:` 콜백입니다.

만약 `urls` 매개 변수가 사용되지 않으면 결과 네트워크 호출은 기본 서비스 공급자 URL을 타겟으로 합니다. Adobe 릴리스/프로덕션 환경입니다.

에 값이 제공된 경우 `urls` 매개 변수, 결과 네트워크 호출은 `urls` 매개 변수. 모든 구성 요청은 별도의 스레드에서 동시에 트리거됩니다. MVPD 목록을 컴파일할 때 첫 번째 응답기가 우선합니다. 목록에 있는 각 MVPD에 대해 AccessEnabler는 연관된 서비스 공급자의 URL을 기억합니다. 이후의 모든 자격 요청은 구성 단계 동안 대상 MVPD와 연결된 서비스 공급자와 연결된 URL로 전달됩니다.

| API 호출: 요청자 구성 |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**사용 가능:** v1.0+ **까지:** v3.0

| API 호출: 요청자 구성 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**사용 가능:** v1.0+ **까지:** v3.0

**매개 변수:**

* *requestorID*: 프로그래머와 연결된 고유 ID입니다. Primetime 인증 서비스에 처음 등록할 때 Adobe에서 할당한 고유 ID를 사이트에 전달합니다.
* *signedRequestorID*: **이 매개 변수는 iOS AccessEnabler 버전 1.2 이상에 있습니다.** 개인 키로 디지털 서명된 요청자 ID의 사본. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*: 선택적 매개 변수; 기본적으로 Adobe 서비스 공급자가 사용됩니다(http://sp.auth.adobe.com/). 이 배열을 사용하면 Adobe에서 제공하는 인증 및 인증 서비스의 끝점을 지정할 수 있습니다(다른 인스턴스는 디버깅 목적으로 사용될 수 있음). 이를 사용하여 여러 Primetime 인증 서비스 공급자 인스턴스를 지정할 수 있습니다. 이때 MVPD 목록은 모든 서비스 공급자의 끝점으로 구성됩니다. 각 MVPD는 가장 빠른 서비스 공급자와 연결됩니다. 즉, 먼저 응답하고 해당 MVPD를 지원하는 공급자입니다.

**참고:** 호출 없이 `serviceProviders` 매개 변수를 사용하면 라이브러리가 기본 서비스 공급자(즉,`https://sp.auth.adobe.com` 프로덕션 프로파일 또는 `https://sp.auth-staging.adobe.com` 용). 만약 `serviceProviders` 매개 변수가 제공되면 URL의 배열이어야 합니다. 지정한 모든 끝점에서 구성 정보를 검색하고 병합됩니다. 서로 다른 서비스 공급자 응답에 중복 정보가 있는 경우 가장 빠른 응답 서버(즉, 가장 짧은 응답 시간이 있는 서버가 우선함)를 위해 충돌이 해결됩니다.

**콜백이 트리거됨:** [`setRequestorComplete:`](#setReqComplete)


[맨 위로..](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey, setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [사용되지 않음] {#setReq_tvos}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 프로그래머의 ID를 설정합니다. Primetime 인증 시스템의 Adobe에 등록하면 각 프로그래머에게 고유 ID가 할당됩니다. 이 설정은 애플리케이션의 수명 주기 동안 한 번만 수행해야 합니다.

서버 응답에는 MVPD 목록과 함께 Programmer의 ID에 첨부된 일부 구성 정보가 포함되어 있습니다. 서버 응답은 AccessEnabler 코드에서 내부적으로 사용됩니다. 작업 상태(즉, 성공/실패)만 를 통해 애플리케이션에 표시됩니다 `setRequestorComplete:` 콜백입니다.

만약 `urls` 매개 변수가 사용되지 않으면 결과 네트워크 호출은 기본 서비스 공급자 URL을 타겟으로 합니다. Adobe 릴리스/프로덕션 환경입니다.

에 값이 제공된 경우 `urls` 매개 변수, 결과 네트워크 호출은 `urls` 매개 변수. 모든 구성 요청은 별도의 스레드에서 동시에 트리거됩니다. MVPD 목록을 컴파일할 때 첫 번째 응답기가 우선합니다. 목록에 있는 각 MVPD에 대해 AccessEnabler는 연관된 서비스 공급자의 URL을 기억합니다. 이후의 모든 자격 요청은 구성 단계 동안 대상 MVPD와 연결된 서비스 공급자와 연결된 URL로 전달됩니다.



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 요청자 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**사용 가능:** v2.0+ **까지:** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 요청자 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**사용 가능:** v2.0+ **까지:** v3.0

**매개 변수:**

* *requestorID*: 프로그래머와 연결된 고유 ID입니다. Primetime 인증 서비스에 처음 등록할 때 Adobe에서 할당한 고유 ID를 사이트에 전달합니다.
* *signedRequestorID*: **이 매개 변수는 iOS AccessEnabler 버전 1.2 이상에 있습니다.** 개인 키로 디지털 서명된 요청자 ID의 사본. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *url*: 선택적 매개 변수; 기본적으로 Adobe 서비스 공급자가 사용됩니다(http://sp.auth.adobe.com/). 이 배열을 사용하면 Adobe에서 제공하는 인증 및 인증 서비스의 끝점을 지정할 수 있습니다(다른 인스턴스는 디버깅 목적으로 사용될 수 있음). 이를 사용하여 여러 Primetime 인증 서비스 공급자 인스턴스를 지정할 수 있습니다. 이때 MVPD 목록은 모든 서비스 공급자의 끝점으로 구성됩니다. 각 MVPD는 가장 빠른 서비스 공급자와 연결됩니다. 즉, 먼저 응답하고 해당 MVPD를 지원하는 공급자입니다.
* secret 및 publicKey: 두 번째 화면 호출에 서명하는 데 사용되는 비밀과 공개 키입니다. 자세한 내용은 [클라이언트 없는 설명서](#create_dev).

호출 없이 `serviceProviders` 매개 변수를 사용하면 라이브러리가 기본 서비스 공급자에서 구성을 검색합니다(즉, `https://sp.auth.adobe.com` 프로덕션 프로필의 경우 https://sp.auth-staging.adobe.com 을 참조하십시오. 만약 `serviceProviders` 매개 변수가 제공되면 URL의 배열이어야 합니다. 지정한 모든 끝점에서 구성 정보를 검색하고 병합됩니다. 서로 다른 서비스 공급자 응답에 중복 정보가 있는 경우 가장 빠른 응답 서버(즉, 가장 짧은 응답 시간이 있는 서버가 우선함)를 위해 충돌이 해결됩니다.

**콜백이 트리거됨:** [`setRequestorComplete:`](#setReqComplete)

[맨 위로..](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 구성 단계가 완료되었음을 애플리케이션에 알리는 AccessEnabler에 의해 트리거되는 콜백입니다. 앱이 자격 요청 발행을 시작할 수 있음을 나타냅니다. 구성 단계가 완료될 때까지 응용 프로그램에서 자격 요청을 실행할 수 없습니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: 요청자 구성 완료</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**사용 가능:** v1.0+

**매개 변수**:

* *상태*: 다음 값 중 하나를 사용할 수 있습니다.
   * `ACCESS_ENABLER_STATUS_SUCCESS` - 구성 단계를 완료했습니다.
   * `ACCESS_ENABLER_STATUS_ERROR` - 구성 단계 실패

**트리거 기준:**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[맨 위로..](#apis)

</br>

### checkAuthentication {#checkAuthN}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 현재 사용자의 인증 상태를 확인합니다.
로컬 토큰 저장소 공간에서 유효한 인증 토큰을 검색하면 됩니다. 이 메서드를 호출하면 네트워크 호출이 수행되지 않습니다. 애플리케이션에서 사용자의 인증 상태를 쿼리하고 그에 따라 UI를 업데이트하는 데 사용됩니다(즉, 로그인/로그아웃 UI 업데이트). 인증 상태는 를 통해 애플리케이션에 전달됩니다 [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) 콜백입니다.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 상태 확인</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수:** 없음

**콜백이 트리거됨:**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[맨 위로..](#apis)

</br>

### getAuthentication, getAuthentication:withData: {#getAuthN}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 전체 인증 워크플로우를 시작합니다. 인증 상태를 확인하면 시작됩니다. 아직 인증되지 않은 경우 인증 흐름 상태 시스템이 시작됩니다.

* 마지막 인증 시도가 성공하면 MVPD 선택 단계를 건너뛰고 [`navigateToUrl:`](#nav2url) 콜백이 트리거됩니다. 응용 프로그램은 이 콜백을 사용하여 MVPD의 로그인 페이지를 사용하여 사용자에게 표시되는 WebView 컨트롤을 인스턴스화합니다. **[참고: Access Enabler 1.5부터는 SDK의 제한 사항으로 인해 이 기능을 사용할 수 없습니다].**
* 마지막 인증 시도가 실패하거나 사용자가 명시적으로 로그아웃한 경우 [`displayProviderDialog:`](#dispProvDialog) 콜백이 트리거됩니다. 애플리케이션이 이 콜백을 사용하여 MVPD 선택 UI를 표시합니다. 또한 AccessEnabler 라이브러리에 사용자의 MVPD 선택을 알리기 위해 를 통해 인증 흐름을 다시 시작해야 합니다 [`setSelectedProvider:`](#setSelProv) 메서드를 사용합니다.

MVPD 로그인 페이지에서 사용자의 자격 증명이 확인되면 사용자가 MVPD의 로그인 페이지에서 인증되는 동안 발생하는 여러 리디렉션 작업을 모니터링해야 합니다. 올바른 자격 증명을 입력하면 WebView 컨트롤은 `ADOBEPASS_REDIRECT_URL` 상수. 이 URL은 WebView에 의해 로드되지 않습니다. 이 URL을 가로채고 이 이벤트를 로그인 단계가 완료되었음을 신호로 해석해야 합니다. 그러면 인증 흐름을 완료하려면 ( [handleExternalURL](#handleExternalURL) 메서드).

마지막으로 인증 상태는 를 통해 애플리케이션에 전달됩니다 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 콜백입니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**사용 가능:** v1.9+

**매개 변수:**

* *forceAutn*: 사용자가 이미 인증되었는지 여부에 관계없이 인증 흐름을 시작해야 하는지 여부를 지정하는 플래그입니다.
* *데이터*: Pay-TV Pass 서비스로 전송될 키-값 쌍으로 구성된 사전. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다.

**콜백이 트리거됨:** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[맨 위로..](#apis)

</br>

### getAuthentication:filter, getAuthentication:withData:andFilter {#getAuthN_filter}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 전체 인증 워크플로우를 시작합니다. 인증 상태를 확인하면 시작됩니다. 아직 인증되지 않은 경우 인증 흐름 상태 시스템이 시작됩니다.

* [presentTvProviderDialog()](#presentTvDialog) 현재 요청자에게 SSO를 지원하는 MVPD가 하나 이상 있는 경우 가 호출됩니다. MVPD가 SSO를 지원하지 않으면 클래식 인증 흐름이 시작되고 필터 매개 변수가 무시됩니다.
* 사용자가 Apple SSO 흐름을 완료하면 [disableTvProviderDialog()](#dismissTvDialog) 이 트리거되고 인증 프로세스가 종료됩니다.

마지막으로 인증 상태는 를 통해 애플리케이션에 전달됩니다 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 콜백입니다.

**사용 가능:** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**매개 변수:**

* *forceAutn*: 사용자가 이미 인증되었는지 여부에 관계없이 인증 흐름을 시작해야 하는지 여부를 지정하는 플래그입니다.
* *데이터*: Pay-TV Pass 서비스로 전송될 키-값 쌍으로 구성된 사전. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다. 
* 필터: Apple SSO 대화 상자에 표시되는 두 개의 MVPD ID 목록이 있는 사전. SSO를 지원하지 않는 모든 MVPD는 무시되지만 주문은 준수됩니다. 사전에는 두 개의 키가 있어야 합니다.
   * TV\_PROVIDERS: 선택기에 표시되어야 하는 모든 MVPD가 있는 목록
   * 추천\_TV\_PROVIDERS: 선택기에서 중요 항목으로 표시되어야 하는 모든 MVPD가 있는 목록입니다. 이 목록의 MVPD는 TV\_PROVIDERS 목록에도 지정해야 합니다.

**사용 가능:** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**매개 변수:**

* *forceAutn*: 사용자가 이미 인증되었는지 여부에 관계없이 인증 흐름을 시작해야 하는지 여부를 지정하는 플래그입니다.
* *데이터*: Pay-TV Pass 서비스로 전송될 키-값 쌍으로 구성된 사전. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다. 
* 필터: Apple SSO 대화 상자에 표시되는 MVPD ID 목록입니다. SSO를 지원하지 않는 모든 MVPD는 무시되지만 주문은 준수됩니다.

**콜백이 트리거됨:** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[맨 위로..](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 사용자가 원하는 MVPD를 선택할 수 있도록 적절한 UI 요소를 인스턴스화해야 한다고 응용 프로그램에 알리기 위해 AccessEnabler에 의해 트리거되는 콜백입니다. 콜백은 선택 UI 패널(예: MVPD의 로고를 가리키는 URL, 친숙한 표시 이름 등)을 올바르게 작성하는 데 도움이 되는 추가 정보가 있는 MVPD 개체 목록을 제공합니다.

사용자가 원하는 MVPD를 선택하면 상위 계층 응용 프로그램이 를 호출하여 인증 흐름을 재개해야 합니다 `setSelectedProvider:` 사용자가 선택한 항목에 해당하는 MVPD의 ID를 전달합니다.

**인증 흐름 중단** - 사용자가 &quot;뒤로&quot; 단추를 누를 수 있는 지점이며 이는 인증 흐름을 중단하는 것과 같습니다. 이 시나리오에서는 애플리케이션이 [setSelectedProvider:](#setSelProv) null을 매개 변수로 전달하여 AccessEnabler에 인증 상태 시스템을 재설정할 수 있는 기회를 제공합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: mvpd 선택 UI 표시</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**사용 가능:** v1.0+

**매개 변수**:

* *mvpds*: MVPD 선택 UI 요소를 만드는 데 사용할 수 있는 MVPD 관련 정보를 포함하는 MVPD 개체 목록입니다.

**트리거 기준:** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[맨 위로..](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 방법은 사용자의 MVPD 선택을 Access Enabler에 알리기 위해 응용 프로그램에서 호출됩니다. 이 방법을 사용하여 인증에 사용되는 서비스 공급자를 선택하거나 변경할 수 있습니다.

선택한 MVPD가 TempPass MVPD인 경우 나중에 getAuthentication()을 호출하지 않아도 해당 MVPD를 자동으로 인증합니다.

getAuthentication() 메서드에 추가 매개 변수가 제공되는 프로모션 임시 패스에서는 사용할 수 없습니다.

전달 시 *null* Access Enabler는 사용자가 인증 흐름을 취소(즉, &quot;뒤로&quot; 단추 누름)한 것으로 간주하여 인증 상태 시스템을 재설정하고 을 호출하여 응답합니다 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 콜백으로 `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` 오류 코드.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 현재 선택한 공급자 설정</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수:** 없음

**콜백이 트리거됨:** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[맨 위로..](#apis)

</br>

#### navigateToUrl: {#nav2url}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명:** 응용 프로그램에서 UIWebView/WKWebView 컨트롤러를 인스턴스화하고 콜백에서 제공하는 URL을 로드하도록 요청하기 위해 AccessEnabler에 의해 트리거되는 콜백 **`url`** 매개 변수. 콜백은 을 전달합니다 **`url`** 인증 끝점의 URL이나 로그아웃 끝점의 URL을 나타내는 매개 변수입니다.

UIWebView/WKWebView로서` `컨트롤러가 여러 리디렉션을 통과하면 애플리케이션이 컨트롤러의 활동을 모니터링하고 컨트롤러가 정의한 특정 사용자 지정 URL을 로드하는 때를 감지해야 합니다 `ADOBEPASS_REDIRECT_URL `상수(예: `adobepass://ios.app`). 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 응용 프로그램에서 인증 또는 로그아웃 흐름이 완료되었으며 컨트롤러를 닫아도 안전하다는 신호로만 해석해야 합니다. 컨트롤러가 이 특정 사용자 지정 URL을 로드하면 애플리케이션이 UIWebView/WKWebView를 닫고 AccessEnabler를 호출해야 합니다 `handleExternalURL:url `API 메서드.

**참고:** 인증 흐름의 경우 사용자가 &quot;뒤로&quot; 단추를 누를 수 있는 지점이며, 이는 인증 흐름을 중단하는 것과 같습니다. 이러한 시나리오에서는 애플리케이션이 [setSelectedProvider:](#setSelProv) 메서드 전달 **`nil`** 를 매개 변수로 사용하여 AccessEnabler에서 인증 상태 시스템을 재설정할 수 있는 기회를 제공합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: mvpd 로그인 페이지 표시</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수**:

* *url*: MVPD의 로그인 페이지를 가리키는 URL

**트리거 기준:** [setSelectedProvider:](#setSelProv)

 

[맨 위로..](#apis)

</br>

#### navigateToUrl:useSVC: {#nav2urlSVC}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명:** AccessEnabler에 의해 트리거되는 콜백입니다. `navigateToUrl:` 콜백으로, 애플리케이션이 이전에 를 통해 수동 SVC(Safari View Controller) 처리를 활성화한 경우 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) MVPD가 SVC(Safari View Controller)를 필요로 하는 경우에만 호출 및 를 호출합니다. 다른 모든 MVPD의 경우 `navigateToUrl:` 콜백이 호출됩니다. 자세한 내용은[iOS SDK 3.2 이상에서 SFSsafariViewController 지원](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) safari SVC(View Controller)를 관리하는 방법에 대한 자세한 정보

와 비슷합니다 `navigateToUrl:` callback `navigateToUrl:useSVC:` AccessEnabler가 응용 프로그램을 인스턴스화하도록 요청하기 위해 트리거됩니다 `SFSafariViewController` 콜백에서 제공된 URL을 로드하기 위해 및 **`url`** 매개 변수. 콜백은 을 전달합니다 **`url`** 인증 끝점의 URL 또는 로그아웃 끝점의 URL을 나타내는 매개 변수와 **`useSVC`** 응용 프로그램이 `SFSafariViewController`.

로서의 `SFSafariViewController` 컨트롤러가 여러 리디렉션을 통과하면 애플리케이션이 컨트롤러의 활동을 모니터링하고 컨트롤러가 정의한 특정 사용자 지정 URL을 로드하는 때를 감지해야 합니다 `application's custom scheme` (예:** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`). 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 응용 프로그램에서 인증 또는 로그아웃 흐름이 완료되었으며 컨트롤러를 닫아도 안전하다는 신호로만 해석해야 합니다. 컨트롤러가 이 특정 사용자 지정 URL을 로드하면 애플리케이션이 `SFSafariViewController` AccessEnabler를 호출하고 `handleExternalURL:url `API 메서드.

**참고:** 인증 흐름의 경우 사용자가 &quot;뒤로&quot; 단추를 누를 수 있는 지점이며, 이는 인증 흐름을 중단하는 것과 같습니다. 이러한 시나리오에서는 애플리케이션이 [setSelectedProvider:](#setSelProv) 메서드 전달 **`nil`** 를 매개 변수로 사용하여 AccessEnabler에서 인증 상태 시스템을 재설정할 수 있는 기회를 제공합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: sfsSafariViewController에 MVPD 로그인 페이지 표시</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**가용성: **v 3.2+

**매개 변수**:

* *url:* MVPD의 로그인 페이지를 가리키는 URL
* *useSVC:* url을 SFSsafariViewController에 로드할지 여부.

**트리거 기준:**[ setOptions:](#setOptions) 이전 [setSelectedProvider:](#setSelProv) 

[맨 위로..](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 응용 프로그램에서 이 메서드를 호출하여 인증 또는 로그아웃 흐름을 완료합니다. 이 메서드는 애플리케이션이 `UIWebView/WKWebView or SFSafariViewController` 컨트롤러가 특정 사용자 지정 URL로 리디렉션됩니다. 애플리케이션이 `SFSafariViewController `컨트롤러가 특정 사용자 지정 URL을 `application's custom scheme` (예:`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), 그렇지 않으면 이 특정 사용자 지정 URL이 `ADOBEPASS_REDIRECT_URL `상수(예: `adobepass://ios.app`).

인증 흐름의 경우 AccessEnabler는 백엔드 서버에서 인증 토큰을 검색하고 토큰 저장소에 로컬로 저장하여 흐름을 완료합니다. AccessEnabler는 `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 성공을 나타내는 상태 코드가 1인 콜백입니다. 이러한 단계를 실행하는 동안 오류가 발생하면 `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> 콜백은 인증 실패를 나타내는 상태 코드 및 해당 오류 코드를 사용하여 트리거됩니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 또는 로그아웃 흐름 완료</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code> (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v3.0+

**매개 변수:** 

* *url*: 에서 차단된 URL ` UIWebView/WKWebView or SFSafariViewController ` 를 문자열로 반환합니다.


**콜백이 트리거됨:** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[맨 위로..](#apis)

</br>

#### getAuthenticationToken - [사용되지 않음] {#getAuthNToken}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 백 엔드 서버에서 인증 토큰을 요청하여 인증 흐름을 완료합니다. 이 메서드는 MVPD 로그인 페이지를 호스팅하는 WebView 컨트롤이 `ADOBEPASS_REDIRECT_URL` 상수.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 토큰 검색</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+ **까지:** v3.0

**매개 변수:** 없음

**콜백이 트리거됨:** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[맨 위로..](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 응용 프로그램에 인증 흐름의 상태를 알리는 AccessEnabler에 의해 트리거되는 콜백입니다. 사용자의 상호 작용이나 기타 예기치 않은 시나리오(예: 네트워크 연결 문제 등)로 인해 이 흐름이 실패할 수 있는 곳이 많습니다. 이 콜백은 인증 흐름의 성공/실패 상태를 응용 프로그램에 알리는 동시에 필요한 경우 실패 이유에 대한 추가 정보를 제공합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: 인증 흐름의 상태 보고</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**사용 가능:** v1.0+

**매개 변수**:

* *상태*: 다음 값 중 하나를 사용할 수 있습니다.
   * `ACCESS_ENABLER_STATUS_SUCCESS` - 인증 흐름을 완료했습니다.
   * `ACCESS_ENABLER_STATUS_ERROR` - 인증 흐름 실패
* *코드*: 실패 이유. If *상태* is `ACCESS_ENABLER_STATUS_SUCCESS`, 그런 다음 *코드* 는 빈 문자열(즉, `USER_AUTHENTICATED` 상수). 실패할 경우 이 매개 변수는 다음 값 중 하나를 사용할 수 있습니다.
   * `USER_NOT_AUTHENTICATED_ERROR` - 사용자가 인증되지 않았습니다. 에 대한 응답으로 [checkAuthentication:](#checkAuthN) 로컬 토큰 캐시에 유효한 인증 토큰이 없는 경우 메서드 호출입니다.
   * `PROVIDER_NOT_SELECTED_ERROR` - 상위 계층 응용 프로그램이 전달된 후 AccessEnabler가 인증 상태 시스템을 재설정합니다. *null* to [`setSelectedProvider:`](#setSelProv) 인증 흐름을 중단하려면  사용자가 인증 흐름을 취소한 것 같습니다(즉, &quot;뒤로&quot; 단추를 누름).
   * `GENERIC_AUTHENTICATION_ERROR` - 네트워크 비가용성 또는 사용자가 인증 흐름을 명시적으로 취소하여 인증 흐름이 실패했습니다.

**트리거 기준:** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[맨 위로..](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 방법은 응용 프로그램에서 사용자가 이미 특정 보호된 리소스를 볼 수 있는 권한이 있는지 확인하는 데 사용됩니다. 이 방법의 주요 목적은 UI 장식에서 사용할 정보를 검색하는 것입니다 **예를 들어, 잠금 및 잠금 해제 아이콘으로 액세스 상태를 나타냅니다.**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 현재 선택한 공급자 설정</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.3+

**매개 변수:**

* *리소스:* 인증을 확인해야 하는 리소스의 배열입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID는 호출에서 리소스 ID와 동일한 제한 사항을 따릅니다. 즉, 프로그래머와 MVPD 또는 미디어 RSS 조각 간에 설정된 합의된 값이어야 합니다.

**콜백이 트리거됨:** [`preauthorizedResources:`](#preauthResources)

[맨 위로..](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 방법은 응용 프로그램에서 사용자가 이미 특정 보호된 리소스를 볼 수 있는 권한이 있는지 확인하는 데 사용됩니다. 이 방법의 주요 목적은 UI 장식 시 사용할 정보를 검색하는 것입니다(예: 잠금 및 잠금 해제 아이콘으로 액세스 상태를 표시). 다음 **캐시** 매개 변수는 내부 캐시가 리소스를 확인하는 데 사용되는지 여부를 제어합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 현재 선택한 공급자 설정</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**사용 가능:** v3.1+

 

**매개 변수:**

* *리소스:* 인증을 확인해야 하는 리소스의 배열입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 `getAuthorization:` 즉, 프로그래머와 MVPD 또는 미디어 RSS 조각 간에 설정된 합의된 값이어야 합니다.
* *캐시:* 리소스를 해결하기 위해 내부 캐시를 사용할지 여부를 지정하는 부울. false인 경우 캐시가 무시되므로 이 API가 호출될 때마다 서버가 호출됩니다.

**콜백이 트리거됨:** [`preauthorizedResources:`](#preauthResources)

[맨 위로..](#apis)

</br>

### preauthorizedResources: {#preauthResources}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명:** 에 의해 트리거된 콜백 `checkPreauthorizedResources:`. 사용자가 이미 볼 수 있는 권한이 있는 리소스 목록을 제공합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 현재 선택한 공급자 설정</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.3+

**매개 변수:**

* `resources`: 사용자가 이미 볼 수 있는 권한이 있는 리소스의 배열입니다.

**트리거 기준:** [`checkPreauthorizedResources:`](#checkPreauth)

 

[맨 위로..](#apis)

</br>

### checkAuthorization: checkAuthorization:withData: {#checkAuthZ}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 방법은 응용 프로그램에서 인증 상태를 확인하는 데 사용됩니다. 먼저 인증 상태를 확인하여 시작됩니다. 인증되지 않은 경우 [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) 콜백이 트리거되고 메서드가 종료됩니다. 사용자가 인증되면 인증 흐름도 트리거됩니다. 자세한 내용은 [`getAuthorization:`](#getAuthZ) 메서드를 사용합니다.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 상태 확인</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 상태 확인</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.9+

**매개 변수:**

* *리소스*: 사용자가 인증을 요청하는 리소스의 ID입니다.
* *데이터*: Pay-TV Pass 서비스로 전송될 키-값 쌍으로 구성된 사전. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다. 

**콜백이 트리거됨:**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[맨 위로..](#apis)

</br>

### getAuthorization:, getAuthorization:withData: {#getAuthZ}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 메서드는 응용 프로그램에서 인증 흐름을 시작하는 데 사용됩니다. 사용자가 아직 인증되지 않은 경우 인증 흐름도 시작합니다. 사용자가 인증되면 AccessEnabler는 인증 토큰(로컬 토큰 캐시에 유효한 인증 토큰이 없는 경우) 및 단기 미디어 토큰에 대한 요청을 계속 실행합니다. 짧은 미디어 토큰을 얻으면 인증 흐름이 완료된 것으로 간주됩니다. 다음 [setToken:forResource:](#setToken) 콜백은 트리거되고 짧은 미디어 토큰은 애플리케이션에 매개 변수로 전달됩니다. 어떤 이유로든 인증이 실패하면 [tokenRequestFailed:forEventType:](#tokenReqFailed) 콜백이 트리거되고 오류 코드/세부 정보가 제공됩니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 인증 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**사용 가능:** v1.9+

**매개 변수:**

* *리소스*: 사용자가 인증을 요청하는 리소스의 ID입니다.
* *데이터*: Pay-TV Pass 서비스로 전송될 키-값 쌍으로 구성된 사전. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다. 

**콜백이 트리거됨:** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**추가적인 콜백이 트리거됨:**\
이 메서드는 다음 콜백을 트리거할 수도 있습니다(인증 흐름도 시작된 경우). `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`\
 
**참고: checkAuthorization 사용: / checkAuthorization:withData: getAuthorization 대신: / getAuthorization:withData: 가능하다면 getAuthorization: / getAuthorization:withData: 메서드는 전체 인증 흐름을 시작하고(사용자가 인증되지 않은 경우) 이로 인해 프로그래머 측에서 복잡한 구현이 발생할 수 있습니다.**

[맨 위로..](#apis)

</br>

### setToken:forResource: {#setToken}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 인증 흐름이 성공적으로 완료되었음을 애플리케이션에 알리는 AccessEnabler에 의해 트리거된 콜백입니다. 단기 미디어 토큰은 매개 변수로도 전달됩니다.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: 인증 흐름을 완료했습니다.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수**:

* *토큰*: 단기 미디어 토큰
* *리소스*: 인증을 받은 리소스

**트리거 기준:** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[맨 위로..](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 인증 흐름이 실패했음을 상위 계층 응용 프로그램에 알리는 AccessEnabler에 의해 트리거되는 콜백입니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: 인증 흐름 실패</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수**:

* *리소스*: 인증을 받은 리소스입니다.
* *코드*: 실패 시나리오와 연관된 오류 코드입니다. 가능한 값:
   * `USER_NOT_AUTHORIZED_ERROR` - 사용자가 주어진 리소스에 대해 권한을 부여할 수 없습니다.
* *설명*: 실패 시나리오에 대한 추가 세부 정보입니다. 이 설명 문자열을 어떤 이유로든 사용할 수 없는 경우 Primetime 인증에서는 빈 문자열을 보냅니다 **(&quot;&quot;)**. \
   MVPD가 이 문자열을 사용하여 사용자 지정 오류 메시지 또는 판매 관련 메시지를 전달할 수 있습니다. 예를 들어, 구독자가 리소스에 대한 권한이 거부되면 MVPD는 다음과 같은 메시지를 보낼 수 있습니다. 현재 패키지에 있는 이 채널에 액세스할 수 없습니다. 패키지를 업그레이드하려면 **여기**.&quot; 이 콜백을 통해 Primetime 인증을 통해 메시지를 Programmer에게 전달하며, Programmer는 이 콜백을 표시하거나 무시할 수 있습니다. Primetime 인증에서는 이 매개 변수를 사용하여 오류가 발생할 수 있는 조건에 대한 알림을 제공할 수도 있습니다. 예를 들어 &quot;공급자의 인증 서비스와 통신하는 동안 네트워크 오류가 발생했습니다.&quot;입니다.

**트리거 기준:** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[맨 위로..](#apis)

</br>

### 로그아웃 {#logout}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 응용 프로그램에서 이 메서드를 호출하여 로그아웃 흐름을 시작합니다. 로그아웃은 사용자가 Primetime 인증 서버 및 MVPD 서버에서 모두 로그아웃해야 한다는 사실로 인해 일련의 HTTP 리디렉션 작업의 결과입니다. AccessEnabler 라이브러리에서 발행한 간단한 HTTP 요청으로 이 흐름을 완료할 수 없으므로 `UIWebView/WKWebView or SFSafariViewController` HTTP 리디렉션 작업을 따를 수 있으려면 컨트롤러가 인스턴스화되어야 합니다.

로그아웃 흐름은 사용자가 `UIWebView/WKWebView or SFSafariViewController`  어떤 식으로든 통제자. 따라서 Adobe은 로그아웃 프로세스 중에 컨트롤을 보이지 않게(즉, 숨김)할 것을 권장합니다.

인증 흐름과 유사한 패턴이 사용됩니다. iOS AccessEnabler는 `navigateToUrl:` 콜백 또는 `navigateToUrl:useSVC:` 를 만들려면 `UIWebView/WKWebView or SFSafariViewController` 콜백에서 제공된 URL을 로드하기 위해 및 `url` 매개 변수. 백엔드 서버에서 로그아웃 끝점의 URL입니다. tvOS AccessEnabler의 경우 `navigateToUrl:` 콜백 또는 `navigateToUrl:useSVC:` 콜백이 호출됩니다.

여러 리디렉션을 거칠 때 애플리케이션은 `UIWebView/WKWebView or SFSafariViewController `제어하고 특정 사용자 지정 URL을 로드하는 때를 감지합니다. 이 특정 사용자 지정 URL은 실제로 유효하지 않으며, 컨트롤러가 실제로 로드하는 것이 아닙니다. 응용 프로그램에서 로그아웃 흐름이 완료되었으며 컨트롤러를 닫아도 안전하다는 신호로만 해석해야 합니다. 컨트롤러가 이 특정 사용자 지정 URL을 로드하면 애플리케이션이 컨트롤러를 닫고 AccessEnabler를 호출해야 합니다 `handleExternalURL:url `API 메서드. 애플리케이션이 `SFSafariViewController `컨트롤러가 특정 사용자 지정 URL을 `application's custom scheme` (예:`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), 그렇지 않으면 이 특정 사용자 지정 URL이 `ADOBEPASS_REDIRECT_URL `상수(예: `adobepass://ios.app`).

마지막으로 AccessEnabler가 [`setAuthenticationStatus()`](#setAuthNStatus) 상태 코드가 0인 콜백으로 로그아웃 흐름의 성공을 나타냅니다.

**참고:** 사용자가 Apple SSO를 사용하여 로그인하면 VSA203 상태가 트리거됩니다. 이러한 경우 사용자는 시스템 설정에서 로그아웃하라는 안내를 받아야 합니다. 응용 프로그램을 다시 시작할 때 재인증이 발생합니다.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 로그아웃 흐름 시작</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수:** 없음

**콜백이 트리거됨:** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[맨 위로..](#apis)

</br>

### getSelectedProvider {#getSelProv}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 메서드를 사용하여 현재 선택한 공급자를 결정합니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 현재 선택한 MVPD 확인</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수:** 없음

**콜백이 트리거됨:** [`selectedProvider:`](#selProv)

[맨 위로..](#apis)

</br>

### selectedProvider {#selProv}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 현재 선택된 MVPD에 대한 정보를 애플리케이션에 전달하는 AccessEnabler에 의해 트리거되는 콜백입니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: 현재 선택한 MVPD에 대한 정보</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수**:

* *mvpd*: 현재 선택한 MVPD에 대한 정보가 포함된 개체

**트리거 기준:** [`getSelectedProvider`](#getSelProv)

[맨 위로..](#apis)

</br>

### getMetadata: {#getMeta}

**파일:** AccessEnabler/headers/AccessEnabler.h

**설명:** 이 방법을 사용하여 AccessEnabler 라이브러리에서 메타데이터로 노출된 정보를 검색합니다. 응용 프로그램은 사전 기반의 정보를 제공하여 이 데이터에 액세스할 수 있습니다 *key* 입력 매개 변수.

프로그래머에게는 두 가지 유형의 메타데이터가 있습니다.

* 정적 메타데이터(인증 토큰 TTL, 인증 토큰 TTL 및 장치 ID) 
* 사용자 메타데이터(사용자 ID, 우편 번호 등 사용자 특정 정보) 인증 및 권한 부여 흐름 중에 MVPD에서 사용자 장치로 전달할 수 있음

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API 호출: 메타데이터에 대한 AccessEnabler 쿼리</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수:**

* *keyDictionary*: 사전 데이터 구조(다음 형식):
   * 키가 `METADATA_OPCODE_KEY` 및 값은 `METADATA_AUTHENTICATION`를 입력하면 인증 토큰 만료 시간을 얻기 위해 쿼리가 수행됩니다.
   * 키가 `METADATA_OPCODE_KEY` 및 값은 `METADATA_AUTHORIZATION` **및**\
      키: `METADATA_RESOURCE_ID_KEY` 및 값은 특정 리소스 ID인 경우 지정된 리소스에 연결된 인증 토큰의 만료 시간을 가져오도록 쿼리가 수행됩니다.
   * 키가 `METADATA_OPCODE_KEY` 및 값은 `METADATA_DEVICE_ID`를 입력하면 현재 장치 id를 가져오도록 쿼리가 수행됩니다. 이 기능은 기본적으로 비활성화되어 있으며 프로그래머는 Adobe에 지원 및 요금에 대한 정보를 문의해야 합니다.
   * 키가 `METADATA_OPCODE_KEY` 및 값은 `METADATA_USER_META` **및** 키: `METADATA_USER_META_KEY` 및 값은 메타데이터의 이름이고, 사용자 메타데이터에 대한 쿼리가 수행됩니다. 사용 가능한 사용자 메타데이터 유형 목록:
      * `zip` - 우편 번호 목록
      * `householdID` - 가구 식별자. MVPD가 하위 계정을 지원하지 않는 경우에는 하위 계정과 동일합니다 `userID`.
      * `maxRating` - 사용자의 최대 자녀 보호 등급 수집
      * `userID` - 사용자 식별자입니다. MVPD가 하위 계정을 지원하고 사용자가 기본 계정이 아닌 경우, `userID` 과(와) 다릅니다. `householdID.`
      * `channelID` - 사용자가 볼 수 있는 채널 목록입니다.
   >[!NOTE]
   >
   >프로그래머가 사용할 수 있는 실제 사용자 메타데이터는 MVPD가 사용할 수 있는 항목에 따라 다릅니다. 이 목록은 Primetime 인증 시스템에 새로운 메타데이터를 사용할 수 있게 되어 추가됨에 따라 확장됩니다.

**콜백이 트리거됨:** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**추가 정보:** [사용자 메타데이터](/help/authentication/user-metadata.md)

[맨 위로..](#apis)

</br>

### presentTVProviderDialog {#presentTvDialog}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 호출 후 AccessEnabler에 의해 트리거되는 콜백[getAuthentication()](#getAuthN) 현재 요청자가 SSO 지원 기능이 있는 하나 이상의 MVPD를 지원하는 경우

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: SSO 흐름 결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v2.0+

**매개 변수**:

* viewController: Apple SSO 대화 상자를 나타냅니다. 이 viewController를 화면에 표시해야 합니다.

**트리거 기준:** [`getAuthentication`](#getAuthN)

**추가 정보:** [iOS/tvOS Single Sign On](#presentTvDialog)

[맨 위로..](#apis)

</br>

### discloseTVProviderDialog {#dismissTvDialog}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 사용자가 Apple SSO 대화 상자를 닫은 후 AccessEnabler에 의해 트리거되는 콜백입니다.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: SSO 흐름 결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v2.0+

**매개 변수**:

* viewController: Apple SSO 대화 상자를 나타냅니다. 이 viewController는 화면에서 제거해야 합니다.

**트리거 기준:** 사용자 작업

**추가 정보:** [iOS/tvOS Single Sign On](#presentTvDialog)

[맨 위로..](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 를 통해 요청된 메타데이터를 전달하는 AccessEnabler에 의해 트리거되는 콜백 [`getMetadata:`](#getMeta) 호출.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>콜백: 메타데이터 검색 요청 결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**사용 가능:** v1.0+

**매개 변수**:

* *메타데이터*: 요청된 메타데이터입니다. 이 값은 `NSString` 정적 메타데이터(인증 TTL, 인증 TTL, 장치 ID)의 경우.  사용자 특정 메타데이터를 요청할 때 복잡한 개체입니다. 이 복잡한 개체는 일반적으로 JSON 페이로드(예: &#39;{&quot;street&quot;: &quot;Main Avenue&quot;, &quot;Building&quot;: [&quot;150&quot;, &quot;320&quot;]}&#39;는 Objective-C에서 NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;building&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;))로 번역됩니다.   샘플 메타데이터 JSON 개체:

```JSON
        {
            updated: 1334243471,
            encrypted: ["encryptedProp"],
            data: {
                zip: ["12345", "34567"],
                maxRating: { 
                    "MPAA": "PG-13",
                    "VCHIP": "TV-Y", 
                    "URL": "http://exam.pl/e/manage/ratings"
                },
                householdID: "3456",
                userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                channelID: ["channel-1", "channel-2"]
            }
```

* *암호화된*: 검색된 메타데이터가 암호화되어 있는지 여부를 지정하는 부울 값입니다. 이 매개 변수는 사용자 메타데이터 요청에 대해서만 중요하며, 항상 암호화되지 않은 상태로 수신되는 정적 메타데이터(예: 인증 TTL)에는 의미가 없습니다. 이 매개 변수가 true로 설정된 경우, Programmer는 Programmer에 있는 Requestor ID 서명에 사용되는 동일한 개인 키(화이트리스트에 있는 Requestor ID 서명에 사용되는 Privacy Key)를 사용하여 RSA 암호 해독을 수행하여 암호화되지 않은 사용자 메타데이터 값을 가져오는 데 사용됩니다 [`setRequestor:setSignedRequestorId:`](#setReq) 및 `setRequestor:setSignedRequestorId:serviceProviders: `호출).

* *key*: 메타데이터 검색 요청을 만드는 데 사용되는 키입니다.

* *인수*: 에 전달된 동일한 사전 [`getMetadata:`](#getMeta) 호출. 애플리케이션이 요청과 응답을 일치시킬 수 있도록 제공됩니다.

**트리거 기준:** [`getMetadata:`](#getMeta)

**추가 정보:** [사용자 메타데이터](/help/authentication/user-metadata.md)


[맨 위로..](#apis)

</br>

### MVPD {#mvpd}

**파일:** AccessEnabler/headers/model/MVPD.h

**설명** MVPD 개체에 대해 설명합니다. MVPD 속성에 대한 정보를 가져오는 데 사용할 수 있습니다.

**사용 가능:** v1.0+ [boardingStatus 속성은 v2.2에서 사용할 수 있습니다] 

**속성**:

* (NSString) ID - MVPD Id입니다.
* (NSString) displayName - MVPD 이름입니다. [선택기에 표시하는 데 사용해야 합니다]
* (NSString) logoURL - MVPD 로고 주소입니다.
* (BOOL) enablePlatformServices - true인 경우 MVPD는 다음과 같은 SSO 서비스를 지원합니다 [Apple SSO](#presentTvDialog).
* (NSString) boardingStatus - 3개의 값을 가질 수 있습니다.
   * nil - MVPD가 Apple SSO를 지원하지 않습니다.
   * 선택 - MVPD가 Apple 선택기에 나타날 수 있지만 Adobe이 인증 흐름을 수행합니다.
   * 지원 - MVPD는 Apple에서 완전히 지원되며 Apple의 SSO 토큰을 사용합니다.

[맨 위로..](#apis)

</br>

## 이벤트 추적 {#tracking}

AccessEnabler는 자격 흐름과 반드시 관련이 없는 추가 콜백을 트리거합니다. 구현 [`sendTrackingData()`](#sendTracking) 콜백 함수는 선택 사항이지만 애플리케이션에서 특정 이벤트를 추적하고 성공/실패한 인증/인증 시도 횟수와 같은 통계를 컴파일할 수 있습니다. 

### sendTrackingData:forEventType: {#sendTracking}

**파일:** AccessEnabler/headers/EntitlementDelegate.h

**설명** 인증/권한 부여 흐름의 완료/실패와 같은 다양한 이벤트가 발생할 수 있음을 애플리케이션에 알리는 AccessEnabler에 의해 트리거되는 콜백입니다. Primetime 인증 1.6을 사용하면 장치 유형, AccessEnabler 클라이언트 유형 및 운영 체제가 [`sendTrackingData()`](#sendTracking). 다음 [`sendTrackingData()`](#sendTracking) 콜백은 이전 버전과 호환됩니다.

**콜백: 이벤트 추적**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**사용 가능:** v1.0+

**참고:** 장치 유형 및 운영 체제는 공용 Java 라이브러리(<http://java.net/projects/user-agent-utils>) 및 사용자 에이전트 문자열입니다. 이 정보는 작업 지표를 장치 카테고리로 분류하는 거친 방법으로만 제공되지만 Adobe이 잘못된 결과에 대해 책임을 지지 않습니다. 따라서 새 기능을 사용하십시오.

* 장치 유형에 사용할 수 있는 값:
   * `computer`
   * `tablet`
   * `mobile`
   * `gameconsole`
   * `unknown`

* AccessEnabler 클라이언트 유형에 사용할 수 있는 값:
   * `flash`
   * `html5`
   * `ios`
   * `android`


**매개 변수**:

* *이벤트*: 추적 중인 이벤트의 코드입니다. 다음 세 가지 가능한 추적 이벤트 유형이 있습니다.
   * **authorizationDetection:** 인증 토큰 요청이 반환될 때마다(이벤트는 `TRACKING_AUTHORIZATION`)
   * **authenticationDetection:** 인증 확인이 발생할 때마다(이벤트는 `TRACKING_AUTHENTICATION`)
   * **mvpdSelection:** 사용자가 MVPD 선택 양식에서 MVPD를 선택하면 `TRACKING_GET_SELECTED_PROVIDER`)
* *데이터*: 보고된 이벤트와 연결된 추가 데이터입니다. 이 데이터는 값 목록 형태로 표시됩니다.

**트리거 기준:** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

의 값 해석 지침 *데이터* 배열:

* trackingEventType의 경우 `TRACKING_AUTHENTICATION:`
   * **0** - 토큰 요청이 성공했는지(true/false) 및 성공했는지 여부:
   * **1** - MVPD ID 문자열
   * **2개** - GUID(md5 해시됨)
   * **3** - 토큰이 이미 캐시에 있음(true/false)
   * **4** - 장치 유형
   * **5개** - AccessEnabler 클라이언트 유형
   * **6** - 운영 체제 유형

* trackingEventType의 경우 `TRACKING_AUTHORIZATION:`
   * **0** - 토큰 요청이 성공했는지(true/false) 및 성공했는지 여부:
   * **1** - MVPD ID
   * **2개** - GUID(md5 해시됨)
   * **3** - 토큰이 이미 캐시에 있음(true/false)
   * **4** - 오류
   * **5개** - 세부 정보
   * **6** - 장치 유형
   * **7** - AccessEnabler 클라이언트 유형
   * **8** - 운영 체제 유형
* trackingEventType의 경우 `TRACKING_GET_SELECTED_PROVIDER:`
   * **0** - 현재 선택한 MVPD의 ID
   * **1** - 장치 유형
   * **2개** - AccessEnabler 클라이언트 유형
   * **3** - 운영 체제 유형

</br>

## 관련 정보 {#related}

* [iOS 통합 Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
* [iOS 기술 개요](/help/authentication/iostvos-sdk-overview.md)
* [자격 흐름](/help/authentication/entitlement-flow.md)
   <!--* [Tracking Data in Primetime authentication](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)-->
