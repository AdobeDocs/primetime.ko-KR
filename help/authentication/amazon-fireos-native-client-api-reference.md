---
title: Amazon FireOS 기본 클라이언트 API 참조
description: Amazon FireOS 기본 클라이언트 API 참조
exl-id: 8ac9f976-fd6b-4b19-a80d-49bfe57134b5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---

# Amazon FireOS 기본 클라이언트 API 참조 {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

</br>

## 소개 {#intro}

이 문서에서는 Adobe Primetime 인증에서 지원되는 Adobe Primetime 인증용 Amazon FireOS SDK에서 노출하는 메서드 및 콜백에 대해 자세히 설명합니다.</span> 여기에 설명된 메서드와 콜백 함수는 AccessEnabler.h 및 EntitlementDelegate.h 헤더 파일에 정의되어 있습니다.

다음을 참조하십시오. <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> 최신 Amazon FireOS AccessEnabler SDK용 

**참고:** Adobe Primetime 인증 팀에서는 Adobe Primetime 인증만 사용할 것을 권장합니다 *공용* API:

- 공개 API를 사용할 수 있습니다 *완전히 테스트됨* 지원되는 모든 클라이언트 유형에 대해 설명합니다. 모든 공개 기능의 경우 각 클라이언트 유형에 연결된 메서드의 해당 버전이 있는지 확인합니다.
- 공개 API는 이전 버전과의 호환성을 지원하고 파트너 통합이 중단되지 않도록 최대한 안정적이어야 합니다. 단, 의 경우 *비*-공개 API는 향후 언제든지 서명을 변경할 수 있는 권한을 보유합니다. 현재 공개 Adobe Primetime 인증 API 호출의 조합을 통해 지원할 수 없는 특정 흐름이 발생하는 경우 알려 주는 것이 가장 좋은 방법입니다. 귀사의 요구를 고려하여 공개 API를 수정하고 안정적인 솔루션을 제공할 수 있습니다.

## Amazon FireOS SDK API {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthoriz된 리소스](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [token요청 실패](#tokenRequestFailed)
- [로그아웃](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetaStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**설명:** Access Enabler 개체를 인스턴스화합니다. 애플리케이션 인스턴스당 하나의 Access Enabler 인스턴스가 있어야 합니다.

| API 호출: 생성자 |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**가용성:** v3.0+


**매개 변수:**

- *appContext*: Amazon Fire OS 애플리케이션 컨텍스트.
- softwareStatement
- redirectUrl : FireOS의 경우, 매개 변수 값이 무시되고 기본 : adobepass://android.app으로 설정됩니다.
- env_url: Adobe 스테이징 환경을 사용하여 테스트하기 위해 env\_url을 &quot;sp.auth-staging.adobe.com&quot;으로 설정할 수 있습니다.

**사용되지 않음:**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**설명:** 프로그래머의 ID를 설정합니다. 각 프로그래머는 Adobe Primetime 인증 시스템에 대한 Adobe 등록 시 고유 ID가 지정됩니다. 이 설정은 응용 프로그램 수명 주기 동안 한 번만 수행해야 합니다.

서버 응답에는 프로그래머의 ID에 첨부된 일부 구성 정보와 함께 MVPD 목록이 포함됩니다. 서버 응답은 Access Enabler에서 내부적으로 사용됩니다. 작업의 상태(즉, SUCCESS/FAIL)만 setRequestorComplete() 콜백을 통해 응용 프로그램에 표시됩니다.

다음과 같은 경우 *url* 매개 변수가 사용되지 않으면 결과 네트워크 호출이 기본 서비스 공급자 URL(Adobe 릴리스/프로덕션 환경)을 타깃팅합니다.

에 대한 값이 제공되는 경우 *url* 매개 변수, 결과 네트워크 호출은에 제공된 모든 URL을 타겟팅합니다. *url* 매개 변수. 모든 구성 요청은 별도의 스레드에서 동시에 트리거됩니다. MVPD 목록을 컴파일할 때 첫 번째 응답자가 우선합니다. 목록에 있는 각 MVPD에 대해 Access Enabler는 관련 서비스 공급자의 URL을 기억합니다. 모든 후속 자격 요청은 구성 단계 동안 대상 MVPD와 쌍을 이룬 서비스 공급자와 연결된 URL로 전달됩니다.

| API 호출: 요청자 구성 |
| --- |
| ```public void setRequestor(String requestorId)``` |


**가용성:**v 3.0+


| API 호출: 요청자 구성 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**가용성:** v3.0+


**매개 변수:**

- *요청자 ID*: 프로그래머와 연결된 고유 ID입니다. Adobe Primetime 인증 서비스에 처음 등록할 때 Adobe이 할당한 고유 ID를 사이트에 전달합니다.
- *url*: 선택적 매개 변수. 기본적으로 Adobe 서비스 공급자가 사용됩니다(http://sp.auth.adobe.com/). 이 배열을 사용하면 Adobe에서 제공하는 인증 및 권한 부여 서비스에 대한 끝점을 지정할 수 있습니다(디버깅 목적으로 다른 인스턴스를 사용할 수 있음). 이 옵션을 사용하여 여러 Adobe Primetime 인증 서비스 공급자 인스턴스를 지정할 수 있습니다. 이렇게 하면 MVPD 목록은 모든 서비스 공급자의 끝점으로 구성됩니다. 각 MVPD는 가장 빠른 서비스 공급자, 즉 먼저 응답하고 해당 MVPD를 지원하는 공급자와 연결됩니다.

**트리거된 콜백:** `setRequestorComplete()`

 

**사용되지 않음:**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**설명:** 구성 단계가 완료되었음을 애플리케이션에 알리는 Access Enabler에 의해 트리거되는 콜백입니다. 앱에서 권한 부여 요청 발급을 시작할 수 있다는 신호입니다. 구성 단계가 완료될 때까지 애플리케이션에서 권한 부여 요청을 실행할 수 없습니다.

| 콜백: 요청자 구성 완료 |
| --- |
| ```public void setRequestorComplete(int status)``` |

**가용성:** v1.0+

**매개 변수:**

- *상태*: 다음 값 중 하나를 사용할 수 있습니다.
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - 구성 단계가 완료되었습니다.
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - 구성 단계 실패

**트리거 기준:** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**설명:** 글로벌 SDK 옵션을 구성합니다. 수락합니다. **맵\&lt;string string=&quot;&quot;>** as a argument인수 . 맵의 값은 SDK에서 수행하는 모든 네트워크 호출과 함께 서버로 전달됩니다.

값은 현재 흐름(인증/권한 부여)과 관계없이 서버에 전달됩니다. 값을 변경하려면 언제든지 이 메서드를 호출할 수 있습니다.

 

| API 호출: setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**가용성:** v3.0+

**매개 변수:**

- *옵션*: 맵\&lt;string string=&quot;&quot;> 글로벌 SDK 옵션을 포함합니다. 현재 다음 옵션을 사용할 수 있습니다.
   - **applicationProfile** - 이 값을 기반으로 서버 구성을 만드는 데 사용할 수 있습니다.
   - **ap\_vi** - Marketing Cloud visitorID입니다. 이 값은 나중에 고급 분석 보고서에 사용할 수 있습니다.
   - **device\_info** - 다음에 설명된 장치 정보 **기기 정보 요리책 전달**

</br>

### checkAuthentication {#checkAuthN}

**설명:** 인증 상태를 확인합니다. 로컬 토큰 저장 공간에서 유효한 인증 토큰을 검색하여 이를 수행합니다. 이 메서드를 호출하면 네트워크 호출이 수행되지 않습니다. 애플리케이션에서 사용자의 인증 상태를 쿼리하고 그에 따라 UI를 업데이트(즉, 로그인/로그아웃 UI 업데이트)하는 데 사용됩니다. 인증 상태는 를 통해 애플리케이션에 전달됩니다. [*setAuthenticationStatus()*](#setAuthNStatus) callback.

MVPD가 &quot;요청자별 인증&quot; 기능을 지원하는 경우 여러 인증 토큰이 장치에 저장될 수 있습니다. 

| API 호출: 인증 상태 확인 |
| --- |
| ```public void checkAuthentication()``` |

**가용성:** v1.0+

**매개 변수:** 없음

**트리거된 콜백:** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**설명:** 전체 인증 워크플로를 시작합니다. 인증 상태를 확인하는 것으로 시작됩니다. 아직 인증되지 않은 경우 인증 흐름 state-machine이 시작됩니다.

- 마지막 인증 시도가 성공하면 MVPD 선택 단계를 건너뛰고 WebView 컨트롤이 사용자에게 MVPD의 로그인 페이지를 제공합니다.
- 마지막 인증 시도가 실패했거나 사용자가 명시적으로 로그아웃한 경우 [*displayProviderDialog()*](#displayProviderDialog) 콜백이 트리거됩니다. 응용 프로그램은 이 콜백을 사용하여 MVPD 선택 UI를 표시합니다. 또한 앱은 를 통해 사용자의 MVPD 선택에 대해 Access Enabler 라이브러리에 알려 인증 흐름을 재개해야 합니다. [setSelectedProvider()](#setSelectedProvider) 메서드를 사용합니다.

MVPD가 &quot;요청자당 인증&quot; 기능을 지원하는 경우 여러 인증 토큰이 장치에 저장될 수 있습니다(프로그래머당 하나).

마지막으로, 인증 상태는 를 통해 애플리케이션에 전달됩니다. *setAuthenticationStatus()* callback.

| API 호출: 인증 흐름을 시작합니다. |
| --- |
| ```public void getAuthentication()``` |

**가용성:** v1.0+

| API 호출: 인증 흐름을 시작합니다. |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**가용성:** v1.0+

**매개 변수:**

- *forceAuthn*: 사용자가 이미 인증되었는지 여부에 상관없이 인증 흐름을 시작할지 여부를 지정하는 플래그입니다.
- *데이터*: Pay-TV 패스 서비스로 보낼 키-값 쌍으로 구성된 맵입니다. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다.

**트리거된 콜백:** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**설명** 사용자가 원하는 MVPD를 선택할 수 있도록 적절한 UI 요소를 인스턴스화해야 함을 응용 프로그램에 알리기 위해 Access Enabler에 의해 트리거된 콜백입니다. 콜백은 MVPD 개체 목록에 선택 UI 패널을 올바르게 구성하는 데 도움이 되는 추가 정보(예: MVPD의 로고, 친숙한 표시 이름 등을 가리키는 URL)를 제공합니다.

사용자가 원하는 MVPD를 선택하면, 상위 계층 애플리케이션은 를 호출하여 인증 흐름을 재개하는 것이 요구된다 *setSelectedProvider()* 사용자 선택에 해당하는 MVPD의 ID를 전달합니다.\
 

| **콜백: MVPD 선택 UI 표시** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**가용성:** v1.0+

**매개 변수**:

- *mvpds*: 응용 프로그램에서 MVPD 선택 UI 요소를 빌드하는 데 사용할 수 있는 MVPD 관련 정보를 포함하는 MVPD 개체의 목록입니다.

**트리거 기준:** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**설명:** 사용자의 MVPD 선택을 Access Enabler에 알리기 위해 애플리케이션에서 이 메서드를 호출합니다. 통과 시 *null* 매개 변수로서 Access Enabler는 현재 MVPD를 null 값으로 재설정합니다.

| **API 호출: 현재 선택한 공급자를 설정합니다.** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**가용성:**v 1.0+

**매개 변수:** 없음

**트리거된 콜백:** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navigateToUrl {#navigagteToUrl}

**설명:** Android SDK의 Access Enabler에서 트리거된 콜백입니다. Amazon FireOS SDK에서는 무시해야 합니다.

| **콜백: MVPD 로그인 페이지 표시** |
| --- |
| ```public void navigateToUrl(String url)``` |

**가용성:** v1.0+

**매개 변수:**

- *url*: MVPD의 로그인 페이지를 가리키는 URL

**트리거 기준:** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**설명:** 백엔드 서버에서 인증 토큰을 요청하여 인증 흐름을 완료합니다. 

| **API 호출: 인증 토큰 검색** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**가용성:** v1.0+

**매개 변수:**

- *쿠키*: Target 도메인에 설정된 쿠키(참조 구현은 SDK의 데모 애플리케이션 참조).

**트리거된 콜백:** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**설명:** 응용 프로그램에 인증 상태를 알리는 Access Enabler에 의해 트리거된 콜백입니다. 사용자의 상호 작용으로 인해 또는 예기치 않은 다른 시나리오(예: 네트워크 연결 문제 등)로 인해 인증 흐름이 실패할 수 있는 경우가 많습니다. 이 콜백은 응용 프로그램에 인증의 성공/실패 상태를 알리는 동시에 필요한 경우 실패 이유에 대한 추가 정보를 제공합니다.

이 콜백은 로그아웃 흐름이 완료될 때도 신호를 보냅니다.

| **콜백: 인증 흐름 상태 보고** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**가용성:** v1.0+

**매개 변수:**

- *상태*: 다음 값 중 하나를 사용할 수 있습니다.
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - 인증 흐름이 완료되었습니다.
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - 인증 흐름 실패
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT` - 로그아웃
- *코드*: 표시된 상태에 대한 사유. If *상태* 은(는) `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`, 그런 다음 *코드* 는 빈 문자열(즉, `AccessEnabler.USER_AUTHENTICATED` 상수). 인증되지 않은 경우 이 매개 변수는 다음 값 중 하나를 사용할 수 있습니다.
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR` - 사용자가 인증되지 않았습니다. 에 대한 응답으로 *checkAuthentication()* 로컬 토큰 캐시에 유효한 인증 토큰이 없는 경우 메서드 호출.
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler가 상위 레이어 애플리케이션을 통과한 후 인증 상태 시스템을 재설정했습니다. *null* 끝 `setSelectedProvider()` 을 클릭하여 인증 흐름을 중단합니다.  사용자가 인증 흐름을 취소한 것 같습니다(즉, &quot;뒤로&quot; 단추 누름).
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR` - 네트워크를 사용할 수 없거나 사용자가 인증 흐름을 명시적으로 취소하는 등의 이유로 인증 흐름이 실패했습니다.
   - `AccessEnabler.LOGOUT` - 로그아웃 작업으로 인해 사용자가 인증되지 않았습니다. 

**트리거 기준:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**설명:** 이 방법은 애플리케이션에서 사용자가 특정 보호된 리소스를 볼 수 있는 권한이 이미 있는지 확인하는 데 사용됩니다. 이 메서드의 주요 목적은 UI를 장식하는 데 사용할 정보를 검색하는 것입니다(예: 잠금 및 잠금 해제 아이콘으로 액세스 상태를 표시).

| **API 호출: 현재 선택한 공급자를 설정합니다.** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**가용성:** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> 다음 `resources` 매개 변수는 권한 부여를 확인해야 하는 리소스 배열입니다.** 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 의 리소스 ID와 동일한 제한이 적용됩니다. `getAuthorization()` 즉, 프로그래머와 MVPD 간에 설정된 합의된 값 또는 미디어 RSS 조각이어야 합니다.

**트리거된 콜백:** `preauthorizedResources()`

</br>

### preauthoriz된 리소스 {#preauthResources}

**설명:** checkPreauthorizedResources()에 의해 트리거된 콜백입니다. 사용자가 이미 볼 수 있는 권한이 있는 리소스 목록을 제공합니다.

| **API 호출: 현재 선택한 공급자를 설정합니다.** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**가용성:**v 1.0+

**매개 변수:** 다음 `resources` 매개 변수는 사용자에게 이미 보기 권한이 부여된 리소스 배열입니다.

**트리거 기준:** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**설명:** 이 메서드는 애플리케이션에서 인증 상태를 확인하는 데 사용됩니다. 먼저 인증 상태를 확인하는 것으로 시작됩니다. 인증되지 않은 경우 *setTokenRequestFailed()* callback이 트리거되고 메서드가 종료됩니다. 사용자가 인증되면 권한 부여 플로우도 트리거됩니다. 다음에서 세부 사항 보기 *getAuthorization()* 메서드를 사용합니다.

| **API 호출: 인증 상태 확인** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**가용성:** v1.0+

| **API 호출: 인증 상태 확인** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**가용성:** v1.0+

**매개 변수:**

- *resourceId*: 사용자가 인증을 요청하는 리소스의 ID입니다.
- *데이터*: Pay-TV 패스 서비스로 보낼 키-값 쌍으로 구성된 맵입니다. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다.

**트리거된 콜백:** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**설명:** 이 메서드는 애플리케이션에서 인증 흐름을 시작하는 데 사용됩니다. 사용자가 아직 인증되지 않은 경우 인증 플로우도 시작합니다. 사용자가 인증되면 Access Enabler는 계속해서 인증 토큰(로컬 토큰 캐시에 유효한 인증 토큰이 없는 경우) 및 단기 미디어 토큰에 대한 요청을 발행합니다. 짧은 미디어 토큰을 얻으면 인증 흐름이 완료된 것으로 간주됩니다. 다음 *setToken()* 콜백이 트리거되고 짧은 미디어 토큰이 애플리케이션에 매개 변수로 전달됩니다. 어떤 이유로든 승인이 실패하면 *tokenRequestFailed()* 콜백이 트리거되고 오류 코드와 세부 정보가 제공됩니다.

| **API 호출: 인증 흐름 시작** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**가용성:** v1.0+

| **API 호출: 인증 흐름 시작** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**가용성:** v1.0+

**매개 변수:**

- *resourceId*: 사용자가 인증을 요청하는 리소스의 ID입니다.
- *데이터*: Pay-TV 패스 서비스로 보낼 키-값 쌍으로 구성된 맵입니다. Adobe은 이 데이터를 사용하여 SDK를 변경하지 않고 향후 기능을 활성화할 수 있습니다. 

**트리거된 콜백:** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **추가 콜백이 트리거됨**  <br>이 메서드는 다음 콜백을 트리거할 수도 있습니다(인증 플로우도 시작된 경우). _setAuthenticationStatus()_, _displayProviderDialog()_ |

**참고: 가능하면 getAuthorization() 대신 checkAuthorization()을 사용하십시오. getAuthorization() 메서드는 전체 인증 흐름을 시작하며(사용자가 인증되지 않은 경우) 이로 인해 프로그래머측의 구현이 복잡해질 수 있습니다.**

</br>

### setToken {#setToken}

**설명:** 인증 흐름이 성공적으로 완료되었음을 응용 프로그램에 알리는 Access Enabler에 의해 트리거된 콜백입니다. 수명이 짧은 미디어 토큰도 매개 변수로 제공됩니다.

| **콜백: 인증 흐름이 완료되었습니다.** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**가용성:**v 1.0+

**매개 변수:**

- *토큰*: 수명이 짧은 미디어 토큰
- *resourceId*: 인증을 받은 리소스

**트리거 기준:** `checkAuthorization(), getAuthorization()`

<br>

### token요청 실패 {#tokenRequestFailed}

**설명:** 인증 플로우가 실패했음을 상위 계층 응용 프로그램에 알리는 Access Enabler에 의해 트리거되는 콜백입니다.

| **Callback: 인증 흐름 실패** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**가용성:** v1.0+

**매개 변수:**

- *resourceId*: 인증을 받은 리소스
- *errorCode*: 실패 시나리오와 연결된 오류 코드. 가능한 값:
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR` - 사용자가 지정된 리소스에 대해 권한을 부여할 수 없습니다.
- *errorDescription*: 실패 시나리오에 대한 추가 세부 정보. 어떤 이유로든 이 설명 문자열을 사용할 수 없는 경우 Adobe Primetime 인증에서 빈 문자열 를 보냅니다. >**(&quot;&quot;)**.  이 문자열은 MVPD에서 사용자 지정 오류 메시지 또는 판매 관련 메시지를 전달하는 데 사용할 수 있습니다. 예를 들어 구독자가 리소스에 대한 권한 부여를 거부하면 MVPD가 다음과 같은 메시지를 보낼 수 있습니다. &quot;현재 패키지의 이 채널에 대한 액세스 권한이 없습니다. 패키지를 업그레이드하려면 여기를 클릭하십시오.&quot; 이 콜백을 통해 Adobe Primetime 인증을 통해 메시지를 프로그래머에게 전달합니다. 프로그래머는 이를 표시하거나 무시할 수 있습니다. Adobe Primetime 인증은 이 매개 변수를 사용하여 오류가 발생했을 수 있는 조건에 대한 알림을 제공할 수도 있습니다. 예를 들어 &quot;공급자의 인증 서비스와 통신할 때 네트워크 오류가 발생했습니다.&quot;와 같은 경우입니다.

**트리거 기준:** `checkAuthorization(), getAuthorization()`

</br>

### 로그아웃 {#logout}

**설명:** 이 메서드를 사용하여 로그아웃 흐름을 시작합니다. 로그아웃은 사용자가 Adobe Primetime 인증 서버와 MVPD의 서버 모두에서 로그아웃해야 하므로 일련의 HTTP 리디렉션 작업의 결과입니다. 

| **API 호출: 로그아웃 흐름 시작** |
| --- |
| ```public void logout()``` |

**가용성:** v1.0+

**매개 변수:** 없음

**트리거된 콜백:** 없음

</br>

### getSelectedProvider {#getSelectedProvider}

**설명:** 이 메서드를 사용하여 현재 선택한 공급자를 결정합니다.

| **API 호출: 현재 선택한 MVPD를 확인합니다.** |
| --- |
| ```public void getSelectedProvider()``` |

**가용성:** v1.0+

**매개 변수:** 없음

**트리거된 콜백:** `selectedProvider()`

</br>

### selectedProvider {#selectedProvider}

**설명:** 현재 선택한 MVPD에 대한 정보를 응용 프로그램에 전달하는 Access Enabler에 의해 트리거된 콜백입니다.

| **Callback: 현재 선택한 MVPD에 대한 정보** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**가용성:** v1.0+

**매개 변수:**

- *mvpd*: 현재 선택한 MVPD에 대한 정보가 포함된 개체

**트리거 기준:** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**설명:** 이 방법을 사용하면 Access Enabler 라이브러리에서 메타데이터로 노출된 정보를 검색할 수 있습니다. 응용 프로그램은 복합 MetadataKey 개체를 제공하여 이 정보에 액세스할 수 있습니다.

| **API 호출: AccessEnabler for metadata 쿼리** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**가용성:** v1.0+

프로그래머가 사용할 수 있는 메타데이터에는 두 가지 유형이 있습니다.

- 정적 메타데이터(인증 토큰 TTL, 인증 토큰 TTL 및 장치 ID) 
- 사용자 메타데이터(사용자 ID 및 우편번호와 같은 사용자별 정보, 인증 및/또는 인증 흐름 동안 MVPD에서 사용자의 장치로 전달됨)

**매개 변수:**

- *metadataKey*: 키 및 args 변수를 캡슐화하는 데이터 구조로서, 다음과 같은 의미가 있습니다.
   - 키가 `METADATA_KEY_TTL_AUTHN` 그런 다음 인증 토큰 만료 시간을 얻기 위해 쿼리가 수행됩니다.
   - 키가 `METADATA_KEY_TTL_AUTHZ` and args에 이름이 = 인 SerializableNameValuePair 개체가 있습니다. `METADATA_ARG_RESOURCE_ID` 및 값 = `[resource_id]`그런 다음 지정된 리소스와 연결된 인증 토큰의 만료 시간을 얻기 위해 쿼리를 만듭니다.
   - 키가 `METADATA_KEY_DEVICE_ID` 그런 다음 현재 장치 id를 얻기 위해 쿼리가 수행됩니다. 이 기능은 기본적으로 비활성화되어 있으며 프로그래머는 사용 권한 및 요금에 대한 정보를 Adobe에 문의해야 합니다.
   - 키가 `METADATA_KEY_USER_META` and args에 이름이 = 인 SerializableNameValuePair 개체가 있습니다. `METADATA_KEY_USER_META` 및 값 = `[metadata_name]`를 입력하면 사용자 메타데이터에 대해 쿼리가 수행됩니다. 사용 가능한 사용자 메타데이터 유형의 현재 목록:
      - `zip` - 우편 번호
      - `householdID` - 세대 식별자. MVPD가 하위 계정을 지원하지 않는 경우에는 다음과 같습니다. `userID`.
      - `maxRating` - 사용자의 최대 자녀 보호 등급
      - `userID` - 사용자 식별자. MVPD가 하위 계정을 지원하고 사용자가 주 계정이 아닌 경우
      - `channelID` - 사용자가 볼 수 있는 채널 목록

프로그래머가 사용할 수 있는 실제 사용자 메타데이터는 MVPD가 사용할 수 있도록 하는 내용에 따라 다릅니다.  이 목록은 새 메타데이터를 사용할 수 있고 Adobe Primetime 인증 시스템에 추가됨에 따라 더 확장됩니다.

**트리거된 콜백:** [`setMetadataStatus()`](#setMetadaStatus)

**추가 정보:** [사용자 메타데이터](#setmetadatastatus)

</br>

### setMetaStatus {#setMetadaStatus}

**설명:** 다음을 통해 요청된 메타데이터를 전달하는 Access Enabler에 의해 트리거된 콜백 *getMetadata()* 호출합니다.

| **Callback: 메타데이터 검색 요청의 결과** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**가용성:** v1.0+

**매개 변수:**

- *key*: 메타데이터 값이 요청되는 키 및 관련 매개 변수가 포함된 MetadataKey 개체입니다(참조 구현은 데모 애플리케이션 참조).
- *결과*: 요청된 메타데이터가 포함된 복합 개체입니다. 개체에는 다음 필드가 있습니다.
   - *simpleResult*: 인증 TTL, 권한 부여 TTL 또는 장치 ID에 대해 요청될 때 메타데이터 값을 나타내는 문자열입니다. 사용자 메타데이터에 대한 요청인 경우 이 값은 null입니다.

   - *사용자 메타데이터 결과*: JSON 사용자 메타데이터 페이로드의 Java 표현을 포함하는 객체입니다. 예:

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
      ```

      는 다음과 같이 Java로 변환됩니다. 

      ```java
      Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
      ```

      **사용자 메타데이터 객체의 실제 구조는 다음과 유사합니다.**

      ```json
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
      }
      ```
 

단순 메타데이터(인증 TTL, 권한 부여 TTL 또는 장치 ID)에 대해 요청되면 이 값은 null입니다.

- *암호화됨*: 검색된 메타데이터의 암호화 여부를 지정하는 부울 값입니다. 이 매개 변수는 사용자 메타데이터 요청에만 중요하며 항상 암호화되지 않은 상태로 수신되는 정적 메타데이터(예: 인증 TTL)에는 의미가 없습니다. 이 매개 변수가 True로 설정되면 프로그래머가 화이트리스트에 있는 개인 키(에서 요청자 ID의 서명에 사용되는 동일한 개인 키)를 사용하여 RSA 암호 해독을 수행하여 암호화되지 않은 사용자 메타데이터 값을 가져옵니다. [`setRequestor`](#setRequestor) 호출).

**트리거 기준:** [`getMetadata()`](#getMetadata)

**추가 정보:** [사용자 메타데이터](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**설명:** 이 메서드를 사용하여 AccessEnabler 현재 버전을 검색합니다.  

| **API 호출: AccessEnabler 버전 가져오기** |
| --- |
| ```public static String getVersion()``` |

## 이벤트 추적 {#tracking}

Access Enabler는 자격 흐름과 관련이 없는 추가 콜백을 트리거합니다. 이라는 이벤트 추적 콜백 함수 구현 *sendTrackingData()* 는 선택 사항이지만 응용 프로그램에서 특정 이벤트를 추적하고 인증/권한 부여에 성공한/실패한 횟수 등의 통계를 컴파일할 수 있도록 합니다. 다음은 의 사양입니다. *sendTrackingData()* callback:

### sendTrackingData {#sendTrackingData}

**설명:** 인증/권한 부여 흐름의 완료/실패와 같은 다양한 이벤트 발생에 대해 응용 프로그램에 보내는 Access Enabler 신호를 통해 트리거되는 콜백입니다. 디바이스 유형, Access Enabler 클라이언트 유형 및 운영 체제도 sendTrackingData()에 의해 보고됩니다.

>[!WARNING]
>
> 장치 유형 및 운영 체제는 공개 Java 라이브러리(http://java.net/projects/user-agent-utils) 및 사용자 에이전트 문자열을 사용하여 파생됩니다. 이 정보는 운영 지표를 장치 범주로 분류하는 거친 방법으로만 제공되지만, 잘못된 결과에 대해서는 Adobe이 책임을 지지 않을 수 있습니다. 그에 따라 새로운 기능을 사용하십시오.

- 장치 유형에 가능한 값:
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- Access Enabler 클라이언트 유형에 사용할 수 있는 값은 다음과 같습니다.
   - `flash`
   - `html5`
   - `ios`
   - `tvos`
   - `android`
   - `firetv`

| 콜백: 이벤트 추적 |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**가용성:** v1.0+

**매개 변수:**

- *이벤트*: 추적 중인 이벤트입니다. 가능한 추적 이벤트 유형에는 세 가지가 있습니다.
   - **authorizationDetection:** 인증 토큰 요청이 반환될 때마다(이벤트 유형: `EVENT_AUTHZ_DETECTION`)
   - **authenticationDiscovery:** 인증 확인이 발생할 때마다(이벤트 유형: `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** 사용자가 MVPD 선택 양식에서 MVPD를 선택하면(이벤트 유형: `EVENT_MVPD_SELECTION`)
- *데이터*: 보고된 이벤트와 관련된 추가 데이터입니다. 이 데이터는 값 목록 형태로 표시됩니다.

다음은 의 값을 해석하기 위한 지침입니다. *데이터* 배열:

- 이벤트 유형 *`EVENT_AUTHN_DETECTION`:*
   - **0** - 토큰 요청의 성공 여부(true/false) 및 위의 내용이 true인 경우:
   - **1** - MVPD ID 문자열
   - **2** - GUID(md5 해시됨)
   - **3** - 토큰이 이미 캐시에 있습니다(true/false).
   - **4** - 장치 유형
   - **5** - 액세스 Enabler 클라이언트 유형
   - **6** - 운영 체제 유형

- 이벤트 유형 `EVENT_AUTHZ_DETECTION`
   - **0** - 토큰 요청의 성공 여부(true/false) 및 성공 여부:
   - **1** - MVPD ID
   - **2** - GUID(md5 해시됨)
   - **3** - 토큰이 이미 캐시에 있습니다(true/false).
   - **4** - 오류
   - **5** - 세부 정보
   - **6** - 장치 유형
   - **7** - 액세스 Enabler 클라이언트 유형
   - **8** - 운영 체제 유형

- 이벤트 유형 `EVENT_MVPD_SELECTION`
   - **0** - 현재 선택한 MVPD의 ID
   - **1** - 장치 유형
   - **2** - 액세스 Enabler 클라이언트 유형
   - **3** - 운영 체제 유형

**트리거 기준:** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
