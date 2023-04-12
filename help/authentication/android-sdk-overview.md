---
title: Android SDK 개요
description: Android SDK 개요
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 0%

---



# Android SDK 개요 {#android-sdk-overview}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>


## 소개 {#intro}

Android AccessEnabler는 모바일 앱에서 TV Everywhere의 자격 서비스에 Adobe Primetime 인증을 사용할 수 있도록 해주는 Java Android 라이브러리입니다. Android 구현은 자격 API를 정의하는 AccessEnabler 인터페이스와 라이브러리가 트리거하는 콜백을 설명하는 EntitlementDelegate 프로토콜로 구성됩니다. 프로토콜과 함께 인터페이스를 사용하는 경우 다음과 같은 공통 이름이 있습니다. AccessEnabler Android 라이브러리입니다.

## Android 요구 사항 {#reqs}

Android 플랫폼 및 Primetime 인증과 관련된 최신 기술 요구 사항은 다음을 참조하십시오 [플랫폼/장치/도구 요구 사항](#android)를 참조하거나 Android SDK 다운로드에 포함된 릴리스 노트를 참조하십시오.

## 기본 클라이언트 워크플로우 이해 {#native_client_workflows}

기본 클라이언트 워크플로우는 일반적으로 브라우저 기반 Primetime 인증 클라이언트의 워크플로우와 동일하거나 매우 유사합니다. 그러나 아래에 설명된 대로 몇 가지 예외가 있습니다.

- [초기화 후 워크플로우](#post-init)
- [일반 초기 인증 워크플로우](#generic)
- [로그아웃 워크플로우](#logout)



### 초기화 후 워크플로우 {#post-init}

AccessEnabler에서 지원하는 모든 자격 부여 워크플로우는 이전에 [`setRequestor()`](#setRequestor) 자신의 정체성을 확립하기 위해 일반적으로 응용 프로그램의 초기화/설정 단계 동안 한 번만 요청자 ID를 제공하도록 이 호출을 수행합니다.


에 대한 초기 호출 후 기본 클라이언트(예: Android)를 사용하여 [`setRequestor()`](#setRequestor)를 선택하는 경우, 다음 절차를 진행할 수 있습니다.

- 권한 부여 호출을 즉시 시작하고 필요한 경우 해당 호출을 자동으로 큐에 올릴 수 있도록 할 수 있습니다.

- 또는 의 성공/실패에 대한 확인을 받을 수 있습니다 [`setRequestor()`](#setRequestor) setRequestorComplete() 콜백을 구현하여

- 아니면 둘 다 해

성공 알림을 기다릴 것인지 여부는 사용자가 결정합니다 [`setRequestor()`](#setRequestor) 또는 AccessEnabler의 호출 큐 메커니즘을 사용합니다. 모든 후속 인증 및 인증 요청에는 요청자 ID와 관련 구성 정보가 필요하므로 [`setRequestor()`](#setRequestor) 초기화가 완료될 때까지 모든 인증 및 인증 API 호출을 효과적으로 차단합니다.

 

### 일반 초기 인증 워크플로우 {#generic}

이 워크플로우의 목적은 MVPD를 사용하여 사용자에게 로그인하는 것입니다.  성공적으로 로그인하면 백엔드 서버가 사용자에게 인증 토큰을 보냅니다. 인증은 일반적으로 인증 프로세스의 일부로 수행되지만, 다음 단계에서는 인증이 격리 상태에서 작동하는 방법에 대해 설명하고 인증 단계를 포함하지 않습니다.

다음 기본 클라이언트 워크플로우는 일반적인 브라우저 기반 인증 워크플로우와 다르지만 기본 클라이언트와 브라우저 기반 클라이언트 모두에 대해 1-5단계가 동일합니다.

1. 페이지 또는 플레이어가 를 호출하여 인증 워크플로우를 시작합니다 [getAuthentication()](#getAuthN): 유효한 캐시된 인증 토큰을 확인하는 것입니다. 이 메서드에는 선택 사항이 있습니다 `redirectURL` parameter; 에 값을 제공하지 않으면 `redirectURL`를 입력하면 인증이 초기화된 URL로 사용자가 반환됩니다.
1. AccessEnabler는 현재 인증 상태를 결정합니다. 사용자가 현재 인증되면 AccessEnabler가 `setAuthenticationStatus()` 성공을 나타내는 인증 상태를 전달하는 콜백 함수(아래 7단계)입니다.
1. 사용자가 인증되지 않은 경우 AccessEnabler는 지정된 MVPD에서 사용자의 마지막 인증 시도가 성공했는지 여부를 확인하여 인증 흐름을 계속합니다. MVPD ID가 캐시되고 `canAuthenticate` 플래그가 true이거나 [`setSelectedProvider()`](#setSelectedProvider)로 설정되어 있는 경우 사용자에게 MVPD 선택 대화 상자가 표시되지 않습니다. 인증 흐름은 MVPD의 캐시된 값(즉, 마지막 성공적인 인증 동안 사용된 것과 동일한 MVPD)을 계속 사용합니다. 백엔드 서버에 네트워크 호출이 수행되고 사용자가 MVPD 로그인 페이지로 리디렉션됩니다(아래 6단계).
1. 캐시된 MVPD ID가 없고 [`setSelectedProvider()`](#setSelectedProvider) 또는 `canAuthenticate` 플래그가 false로 설정되어 있고, [`displayProviderDialog()`](#displayProviderDialog) 콜백이 호출됩니다. 이 콜백은 페이지 또는 플레이어에서 사용자가 선택할 MVPD 목록을 표시하는 UI를 만들도록 안내합니다. MVPD 선택기를 만드는 데 필요한 정보가 포함된 MVPD 개체 배열이 제공됩니다. 각 MVPD 개체는 MVPD 엔터티에 대해 설명하고 MVPD의 ID(예: XFINITY, AT\&amp;T 등)와 같은 정보를 포함합니다. 및 MVPD 로고가 있는 URL입니다.
1. 특정 MVPD를 선택하면 페이지나 플레이어에서 사용자가 선택한 내용을 AccessEnabler에 알려야 합니다. Flash이 아닌 클라이언트의 경우 사용자가 원하는 MVPD를 선택하면 AccessEnabler에 대한 호출을 통해 사용자 선택을 알려줍니다 [`setSelectedProvider()`](#setSelectedProvider) 메서드를 사용합니다. 대신 Flash 클라이언트가 공유 를 발송합니다. `MVPDEvent` 유형 &quot;`mvpdSelection`&quot;. 선택한 공급자를 전달합니다.
1. Android 애플리케이션의 경우 com.android.chrome을 사용할 수 있는 경우 Chrome 사용자 지정 탭에 인증 url이 로드됩니다.
1. Chrome 사용자 지정 탭을 통해 사용자가 MVPD의 로그인 페이지에 도달하여 자격 증명을 입력합니다. 이 전송 중에 여러 리디렉션 작업이 발생합니다.
1. Chrome 사용자 지정 탭에서 url이 리소스 &quot;redirect\_uri&quot;(즉, adobepass://com.adobepass )의 스키마(adobepass://) 및 딥 링크와 일치하는지 확인하면 AccessEnabler는 백엔드 서버에서 실제 인증 토큰을 검색합니다. 최종 리디렉션 URL은 실제로 유효하지 않으며 Chrome 사용자 지정 탭에서 실제로 로드되도록 하지 않습니다. 인증 흐름이 완료되었음을 알리는 신호로만 SDK에서 해석해야 합니다.
1. AccessEnabler는 인증 흐름이 완료되었음을 애플리케이션에 알려줍니다. AccessEnabler가 [`setAuthenticationStatus()`](#setAuthNStatus) 성공을 나타내는 상태 코드가 1인 콜백입니다. 이러한 단계를 실행하는 동안 오류가 발생하면 [`setAuthenticationStatus()`](#setAuthNStatus) 콜백은 인증 실패를 나타내는 해당 오류 코드와 함께 0이라는 상태 코드와 함께 트리거됩니다.

### 로그아웃 워크플로우 {#logout}

기본 클라이언트의 경우 로그아웃은 위에서 설명한 인증 프로세스와 유사하게 처리됩니다. 이 패턴에 따라 AccessEnabler는 Chrome 사용자 지정 탭을 열고 백엔드 서버에서 로그아웃 끝점의 URL을 로드합니다.



**참고:** 한 Programmer/MVPD 세션에서 로그아웃하면 해당 장치에서 SSO를 통해 얻은 다른 모든 Programmer 인증 토큰을 포함하여 해당 특정 MVPD에 대한 기본 저장소가 지워집니다. 다른 MVPD에 대해 획득되었거나 SSO를 통해 획득되지 않은 토큰은 삭제되지 않습니다. 


## 토큰 {#tokens}

- [정의 및 사용](#definitions)
- [캐싱 지침](#caching)
- [지속성](#persistence)
- [형식](#format)
- [장치 바인딩](#device_binding)



### 정의 및 사용 {#definitions}

Primetime 인증 자격 솔루션은 인증 및 인증 워크플로우가 성공적으로 완료될 때 Primetime 인증이 생성하는 특정 데이터(토큰)의 생성을 다룹니다. 이러한 토큰은 클라이언트의 Android 장치에 로컬로 저장됩니다.

토큰은 수명이 제한됩니다. 만료 시 인증 및/또는 인증 워크플로우의 재시작을 통해 토큰을 다시 발급해야 합니다.

권한 부여 워크플로우 동안 발행된 토큰은 세 가지 유형이 있습니다.

- **인증 토큰** - 사용자 인증 워크플로우의 최종 결과는 AccessEnabler가 사용자를 대신하여 인증 쿼리를 수행하는 데 사용할 수 있는 인증 GUID입니다. 이 인증 GUID에는 사용자의 인증 세션 자체와 다를 수 있는 연결된 TTL(Time-to-Live) 값이 있습니다. Primetime 인증은 인증 요청을 시작하는 장치에 인증 GUID를 바인딩하여 인증 토큰을 생성합니다.
- **인증 토큰** - 고유한 로 식별되는 특정 보호된 리소스에 대한 액세스 권한을 부여합니다 `resourceID`. 인증 기관에서 발행한 승인 부여 원본 `resourceID`. 이 정보는 요청을 시작하는 장치에 바인딩됩니다.
- **단기 미디어 토큰** - AccessEnabler는 단기 미디어 토큰을 반환하여 주어진 리소스에 대한 호스팅 애플리케이션에 대한 액세스 권한을 부여합니다. 이 토큰은 해당 특정 리소스에 대해 이전에 획득한 인증 토큰을 기반으로 생성됩니다. 또한 이 토큰이 장치에 바인딩되지 않으며 연결된 수명 범위가 훨씬 짧습니다(기본값: 5분)

인증 및 인증이 성공하면 Primetime 인증은 인증, 인증 및 수명이 짧은 미디어 토큰을 발행합니다. 이러한 토큰은 사용자의 장치에 캐시되고 연관된 수명 동안 사용되어야 합니다.



### 캐싱 지침 {#caching}

- 인증 토큰
- 인증 토큰
- 미디어 토큰


#### 인증 토큰

- **AccessEnabler 1.6 이상** - **** 장치에서 인증 토큰을 캐시하는 방법은 &quot;**요청자별 인증&quot;** 현재 MVPD와 연결된 플래그:


1. 요청자별 인증 기능이 *비활성화됨*&#x200B;를 지정하면 단일 인증 토큰이 글로벌 대지에 로컬로 저장됩니다. 이 토큰은 현재 MVPD와 통합된 모든 응용 프로그램 간에 공유됩니다.
1. 요청자별 인증 기능이 *활성화됨*&#x200B;그러면 토큰이 인증 흐름을 수행한 프로그래머와 명시적으로 연결됩니다(토큰은 글로벌 대지에 저장되지 않고 해당 프로그래머 응용 프로그램에만 표시되는 개인 파일). 특히 서로 다른 응용 프로그램 간의 SSO(Single Sign-On)가 비활성화됩니다. 사용자는 새 앱으로 전환할 때 인증 흐름을 명시적으로 수행해야 합니다(두 번째 앱의 프로그래머가 현재 MVPD와 통합되고 로컬 캐시에 해당 프로그래머에 대한 인증 토큰이 없음).

   **참고:** AEM 1.6 Google GSON 기술 참고: [Gson 종속성을 해결하는 방법](https://tve.zendesk.com/entries/22902516-Android-AccessEnabler-1-6-How-to-resolve-Gson-dependencies)

- **AccessEnabler 1.7** - 이 SDK에서는 여러 Programmer-MVPD 버킷을 사용할 수 있는 새로운 토큰 저장 방법을 도입하여 여러 인증 토큰을 제공합니다. AEM 1.7에서는 &quot;요청자별 인증&quot; 시나리오 및 일반적인 인증 플로우에 대해 동일한 스토리지 레이아웃이 사용됩니다. 두 방법 간의 유일한 차이점은 인증이 수행되는 방식입니다. &quot;요청자별 인증&quot;에는 AccessEnabler가 스토리지(다른 프로그래머용)에 인증 토큰이 존재함에 따라 백 채널 인증을 수행할 수 있는 새로운 개선 사항(수동 인증)이 포함되어 있습니다. 사용자는 한 번만 인증해야 하며 이 세션은 후속 앱에서 인증 토큰을 가져오는 데 사용됩니다. 이 백 채널 플로우는 [`setRequestor()`](#setRequestor) 은 Programmer에게 거의 투명합니다. 여기에 단 하나의 중요한 요구 사항이 있습니다. 프로그래머 MUST 호출 [`setRequestor()`](#setRequestor) 기본 UI 스레드와 활동 내에서 을 선택할 수 있습니다. 


#### 인증 토큰

지정된 순간에 AccessEnabler에서 리소스당 하나의 인증 토큰만 캐시됩니다. 캐시된 인증 토큰이 여러 개 있을 수 있지만 서로 다른 리소스와 연결되어 있습니다. 새 인증 토큰이 발급되고 동일한 리소스에 대해 이전 인증 토큰이 이미 있을 때마다 새 토큰이 기존의 캐시된 값을 덮어씁니다.



#### 미디어 토큰 

단기 미디어 토큰은 캐시하면 안 됩니다. 미디어 토큰은 일회용 사용으로 제한되므로 인증 API가 호출될 때마다 서버에서 검색해야 합니다.



### 지속성 {#persistence}

토큰은 동일한 애플리케이션의 연속된 실행에서 지속되어야 합니다. 즉, 인증 및 인증 토큰이 획득되고 사용자가 애플리케이션을 닫으면 사용자가 애플리케이션을 다시 열 때 동일한 토큰을 애플리케이션에서 사용할 수 있습니다. 또한 여러 애플리케이션에서 이러한 토큰을 유지하는 것이 좋습니다. 즉, 사용자가 하나의 애플리케이션을 사용하여 특정 ID 공급자와 로그인(인증 및 인증 토큰을 성공적으로 획득)한 후 다른 애플리케이션을 통해 동일한 토큰을 사용할 수 있으며, 동일한 ID 공급자를 통해 로그인할 때 사용자에게 자격 증명을 묻는 메시지가 더 이상 표시되지 않습니다.



이러한 유형의 원활한 인증/인증 워크플로우가 Primetime 인증 솔루션을 진정한 TV-Every 구현으로 만드는 이유입니다. 순수 엔지니어링 관점에서 볼 때 Android AccessEnabler 라이브러리는 토큰 데이터를 외부 스토리지에 있는 데이터베이스 파일에 저장하여 애플리케이션 간 데이터 공유 문제를 해결합니다. 이 시스템 수준 공유 리소스는 원하는 영구 토큰 사용 사례를 구현할 수 있는 주요 요소를 제공합니다.

- 구조화된 스토리지 지원 - Primetime 인증 토큰 스토리지는 단순한 선형 버퍼와 같은 메모리 구조가 아닙니다. 사용자가 지정한 키 값을 기반으로 데이터 색인화를 허용하는 사전 같은 저장 메커니즘을 제공합니다.
- 기본 파일 시스템을 사용한 데이터 지속성 지원 - 데이터베이스 파일의 내용은 기본적으로 유지되며 데이터는 장치의 외부 메모리에 저장됩니다.



특정 토큰을 토큰 캐시에 배치하면 AccessEnabler 라이브러리에서 다른 시간에 해당 유효성을 검사합니다.  유효한 토큰은 다음과 같이 정의됩니다.

- 토큰의 TTL이 만료되지 않았습니다
- 토큰의 발급자는 허용된 ID 공급자 목록에 포함됩니다



AccessEnabler 1.7부터 토큰 스토리지는 여러 Programmer-MVPD 조합을 지원할 수 있으며, 여러 인증 토큰을 보유할 수 있는 다중 수준의 중첩 맵 구조에 의존합니다. 이 새 스토리지는 어떤 식으로든 AccessEnabler 공용 API에 영향을 주지 않으며 프로그래머 측에서 변경할 필요가 없습니다. 다음은 이러한 최신 기능을 보여주는 예입니다.

1. App1(Programmer1에서 개발)을 엽니다.
1. MVPD1을 인증합니다(Programmer1과 통합).
1. 현재 응용 프로그램을 일시 중단/닫고 App2(Programmer2에서 개발)를 엽니다.
1. Programmer2가 MVPD2와 통합되지 않았다고 가정해 보겠습니다. 따라서 사용자는 App2에서 인증되지 않습니다.
1. App2에서 MVPD2(Programmer2와 통합)로 인증합니다.
1. 다시 App1으로 전환합니다. 사용자는 여전히 Programmer1로 인증됩니다.

이전 버전의 AccessEnabler에서는 토큰 저장소가 이전에 한 개의 인증 토큰만 지원했기 때문에 6단계에서 사용자가 인증되지 않은 것으로 렌더링됩니다.


**참고:** 하나의 Programmer/MVPD 세션에서 로그아웃하면 SSO를 사용하는 장치에서 다른 모든 Programmer 인증 토큰을 포함하여 기본 저장소가 지워집니다. 다른 MVPD에 대해 획득되었거나 SSO를 통해 획득되지 않은 토큰은 삭제되지 않습니다. 인증 흐름 취소(호출 중) [`setSelectedProvider(null)`](#setSelectedProvider))은 기본 저장소를 지우지 않지만 현재 Programmer/MVPD 인증 시도(현재 Programmer의 MVPD를 지우는 방법)에만 영향을 줍니다.


AccessEnabler 1.7에 포함된 다른 스토리지 관련 기능을 사용하면 이전 스토리지 영역에서 인증 토큰을 가져올 수 있습니다. 이 &quot;토큰 가져오기&quot;를 사용하면 스토리지 버전을 업그레이드할 때에도 SSO 상태를 유지하면서 연속 AccessEnabler 릴리스 간의 호환성을 유지할 수 있습니다. 

가져오기 프로그램은 [`setRequestor()`](#setRequestor) 현재 저장소에 현재 Programmer에 대한 유효한 인증 토큰이 없다고 가정할 경우 다음 두 가지 시나리오에서 실행됩니다.

- 특정 프로그래머가 개발한 1.7 앱의 첫 번째 설치
- 새 스토리지를 사용하는 향후 AccessEnabler로 경로 업그레이드

가져오기 작업은 Programmer에 투명하며 클라이언트 응용 프로그램에서 코드를 변경할 필요가 없습니다.



### 형식 {#format}

- [인증 토큰](#authn_token)
- [인증 토큰](#authz_token)
- [Short Media 토큰](#short_media_token)
- [장치 바인딩](#device_binding)

#### 인증 토큰 {#authn_token}

아래 목록은 인증 토큰의 형식을 나타냅니다.

```XML
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

```XML
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


#### Short Media 토큰 {#short_media_token}

아래 목록은 짧은 미디어 토큰의 형식을 제공합니다.  이 토큰은 Programmer의 응용 프로그램에 노출됩니다.  성공적인 자격 부여 프로세스가 끝나면 Programmer의 애플리케이션에 전달됩니다.

```XML
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
 

#### 장치 바인딩 {#device_binding}

위의 XML 목록에서 태그가 지정된 내용을 확인합니다 `simpleTokenFingerprint`. 이 태그의 목적은 기본 장치 ID 개인화 정보를 보유하는 것입니다. AccessEnabler 라이브러리는 자격 부여 호출 동안 이러한 개인화 정보를 가져와 Primetime 인증 서비스에서 사용할 수 있도록 할 수 있습니다. 서비스는 이 정보를 사용하여 실제 토큰에 포함하므로 토큰을 특정 장치에 효과적으로 결합합니다. 이 방법의 최종 목표는 여러 장치에서 토큰을 전송할 수 없도록 만드는 것입니다.



위의 XML 목록에서 simpleTokenFingerprint 라는 태그를 확인합니다. 이 태그의 목적은 기본 장치 ID 개인화 정보를 보유하는 것입니다. AccessEnabler 라이브러리는 자격 부여 호출 동안 이러한 개인화 정보를 가져와 Primetime 인증 서비스에서 사용할 수 있도록 할 수 있습니다. 서비스는 이 정보를 사용하여 실제 토큰에 포함하므로 토큰을 특정 장치에 효과적으로 결합합니다. 이 방법의 최종 목표는 여러 장치에서 토큰을 전송할 수 없도록 만드는 것입니다.



이 기능은 분명히 보안 관련 기능이므로 보안 관점에서 볼 때 이 정보는 기본적으로 &quot;중요&quot;입니다. 따라서, 이러한 정보는 조작 및 도청은 물론 보호되어야 한다. HTTPS 프로토콜을 통해 인증/승인 요청을 보내어 도청문제가 해결됩니다. 위조 방지 장치는 장치 식별 정보에 디지털 서명을 하여 처리됩니다. AccessEnabler 라이브러리는 장치에서 제공한 정보에서 장치 ID를 계산한 다음 장치 ID를 &quot;clear in the Primetime 인증 서버&quot;에 요청 매개 변수로 전송합니다.  Primetime 인증 서버는 Adobe의 개인 키로 장치 ID에 디지털 서명을 하고 AccessEnabler로 반환되는 인증 토큰에 추가합니다. 따라서 장치 ID가 인증 토큰과 바인딩된다.  인증 흐름 중에 AccessEnabler는 인증 토큰과 함께 장치 ID를 다시 클리어 보냅니다.  유효성 검사 프로세스가 실패하면 인증/인증 워크플로우가 자동으로 실패합니다.  Primetime 인증 서버는 개인 키를 장치 ID에 적용하고 인증 토큰의 값과 비교합니다.  일치하지 않으면 자격 흐름이 실패합니다.


<!--
## Related Information {#related}

- [Android Integration Cookbook](#)
- [Android API](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime authentication native SDK (Tech Note)](#)
- [AE 1.6: How to resolve Gson dependencies (Tech Note)](#)
-->
