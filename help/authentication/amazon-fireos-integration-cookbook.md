---
title: Amazon FireOS 통합 Cookbook
description: Amazon FireOS 통합 Cookbook
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---


# Amazon FireOS 통합 Cookbook {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>


## 소개 {#intro}

이 문서에서는 Amazon FireOS AccessEnabler 라이브러리에 의해 노출된 API를 통해 Programmer의 상위 수준 애플리케이션에서 구현할 수 있는 자격 부여 워크플로우를 설명합니다.

Amazon FireOS용 Adobe Primetime 인증 자격 솔루션은 궁극적으로 두 도메인으로 분할됩니다.

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

AccessEnabler의 네트워크 작업은 다른 스레드에서 수행되므로 UI 스레드가 차단되지 않습니다. 따라서 두 애플리케이션 도메인 간의 양방향 통신 채널은 완전히 비동기적인 패턴을 따라야 합니다.

- UI 애플리케이션 계층은 AccessEnabler 라이브러리에 의해 노출된 API 호출을 통해 AccessEnabler 도메인에 메시지를 보냅니다.
- AccessEnabler는 UI 계층이 AccessEnabler 라이브러리에 등록하는 AccessEnabler 프로토콜에 포함된 콜백 메서드를 통해 UI 레이어에 응답합니다.

## 자격 흐름 {#entitlement}

1. [전제 조건](#prereqs)
1. [시작 흐름](#startup_flow)
1. [인증 흐름](#authn_flow)
1. [인증 흐름](#authz_flow)
1. [미디어 흐름 보기](#media_flow)
1. [로그아웃 흐름](#logout_flow)

 

### A. 사전 요구 사항 {#prereqs}

1. 콜백 함수를 만듭니다.
   - [&#39;setRequestorComplete()&#39;](#$setRequestorComplete)

      - 트리거된 사람 `setRequestor()`성공 또는 실패를 반환합니다.     성공 은 자격 호출을 계속 진행할 수 있음을 나타냅니다.
   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      - 트리거된 사람 `getAuthentication()` 사용자가 공급자(MVPD)를 선택하지 않았고 아직 인증되지 않은 경우에만 해당합니다. 다음 `mvpds` 매개 변수는 사용자가 사용할 수 있는 공급자 배열입니다.
   - [&#39;setAuthenticationStatus(status, reason)&#39;](#$setAuthNStatus)

      - 트리거된 사람 `checkAuthentication()` 항상 트리거된 사람 `getAuthentication()` 사용자가 이미 인증되고 공급자를 선택한 경우에만 해당됩니다.

      - 반환된 상태는 인증되거나 인증되지 않습니다. 그 이유는 인증 실패 또는 로그아웃 작업을 설명합니다.
   - [navigateToUrl(url)](#$navigateToUrl)

      - AmazonFireOS SDK에서 무시된 메서드는 가 트리거되는 Android 플랫폼에서 사용됩니다. `getAuthentication()` 사용자가 MVPD를 선택하면  다음 `url` 매개 변수는 MVPD의 로그인 페이지 위치를 제공합니다.
   - [&#39;sendTrackingData(event, data)&#39;](#$sendTrackingData)

      - 트리거된 사람 `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
다음 `event` 매개 변수는 어떤 자격 이벤트가 발생했는지 나타냅니다; `data` 매개 변수는 이벤트와 관련된 값 목록입니다. 
   - [&#39;setToken(token, resource)&#39;](#$setToken)

      - 트리거된 사람 `checkAuthorization()` 및 `getAuthorization()` 리소스를 볼 수 있는 권한이 성공적으로 부여된 후.
      - 다음 `token` 매개 변수는 단기 미디어 토큰입니다. `resource` 매개 변수는 사용자가 볼 수 있는 권한이 있는 콘텐츠입니다.
   - [&#39;tokenRequestFailed(resource, code, description)&#39;](#$tokenRequestFailed)

      - 트리거된 사람 `checkAuthorization()` 및 `getAuthorization()` 승인 실패 후.
      - 다음 `resource` 매개 변수는 사용자가 보려고 하는 콘텐츠입니다. a `code` 매개 변수는 발생한 실패 유형을 나타내는 오류 코드입니다. a `description` 매개 변수는 오류 코드와 연관된 오류를 설명합니다.
   - [&#39;selectedProvider(mvpd)&#39;](#$selectedProvider)

      - 트리거된 사람 `getSelectedProvider()`.
      - 다음 `mvpd` 매개 변수는 사용자가 선택한 공급자에 대한 정보를 제공합니다.
   - [&#39;setMetadataStatus(메타데이터, 키, 인수)&#39;](#$setMetadataStatus)

      - 트리거된 사람 `getMetadata().`
      - 다음 `metadata` 매개 변수는 요청한 특정 데이터를 제공합니다. a `key` 매개 변수는 `getMetadata()` 요청; 그리고 `arguments` 매개 변수는 에 전달된 것과 동일한 사전입니다 `getMetadata()`.
   - [&#39;preauthorizedResources(resources)&#39;](#$preauthResources)

      - 트리거된 사람 `checkPreauthorizedResources()`.
      - 다음 `authorizedResources` 매개 변수는 사용자가 볼 수 있는 권한이 있는 리소스를 나타냅니다.\
          










![](assets/android-entitlement-flows.png)\
 

### B. 시작 흐름 {#startup_flow}

1. 상위 수준 응용 프로그램을 시작합니다.
1. Adobe Primetime 인증 시작
   1. 호출 [`getInstance`](#$getInstance) Adobe Primetime 인증 AccessEnabler의 단일 인스턴스를 생성하려면

      - **종속성:** Adobe Primetime 인증 네이티브 Amazon FireOS 라이브러리(AccessEnabler)
   2. 호출` setRequestor()` 프로그래머의 신원을 확인하기 위해 프로그래머에게 `requestorID` 및 (선택 사항) Adobe Primetime 인증 엔드포인트의 배열입니다.

      - **종속성:** 유효한 Adobe Primetime 인증 요청자 ID(Adobe Primetime 인증 계정 관리자와 함께 이 항목을 정렬합니다.)

      - **트리거:** setRequestorComplete() 콜백

   요청자 ID가 완전히 설정될 때까지 자격 요청을 완료할 수 없습니다. 따라서 setRequestor() 가 여전히 실행 중이면 이후의 모든 권한 요청(예:`checkAuthentication()`)이 차단되었습니다.

   다음 두 가지 구현 옵션이 있습니다. 요청자 식별 정보가 백엔드 서버로 전송되면 UI 애플리케이션 계층은 다음 두 가지 방법 중 하나를 선택할 수 있습니다.</p>

   1. 의 트리거링을 기다립니다. `setRequestorComplete()` 콜백(AccessEnabler 위임의 일부)  이 옵션은 `setRequestor()` 완료되었으므로 대부분의 구현에 권장됩니다.

   1. 트리거할 때까지 기다리지 않고 계속 진행합니다 `setRequestorComplete()` 콜백하고 권한 요청 실행을 시작합니다. 이러한 호출(checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout)은 AccessEnabler 라이브러리에서 큐에 대기 중입니다. 이 라이브러리는 `setRequestor()`. 예를 들어 네트워크 연결이 불안정할 경우 이 옵션이 가끔 중단될 수 있습니다.




1. 호출 [checkAuthentication()](#$checkAuthN) 전체 인증 흐름을 시작하지 않고 기존 인증을 확인합니다.  이 호출이 성공하면 인증 흐름을 직접 진행할 수 있습니다.  없는 경우 인증 플로우로 진행합니다.

- **종속성:** 에 대한 성공적인 호출 `setRequestor()` (이 종속성은 모든 후속 호출에도 적용됩니다.)

- **트리거:** setAuthenticationStatus() 콜백

### C. 인증 흐름 {#authn_flow}

1. 호출 [`getAuthentication()`](#$getAuthN) 인증 흐름을 시작하거나 사용자가 이미 인증되었음을 확인합니다. 

   **트리거:**  

   - 사용자가 이미 인증된 경우 setAuthenticationStatus() 콜백입니다.  이 경우 로 바로 이동합니다 [인증 흐름](#authz_flow).
   - 사용자가 아직 인증되지 않은 경우 displayProviderDialog() 콜백입니다.  

1. 사용자에게 전송된 공급자 목록을 제공합니다. `displayProviderDialog()`.

1. 사용자가 공급자를 선택하면 WebView에서 사용자가 로그인할 수 있는 공급자 페이지가 열립니다

   **참고:** 이때 사용자는 인증 흐름을 취소할 수 있습니다. 이러한 경우 AccessEnabler가 내부 상태를 정리하고 인증 흐름을 재설정합니다.

1. 사용자가 성공적으로 로그인하면 WebView가 닫힙니다.

1. 호출 `getAuthenticationToken(),` AccessEnabler가 백엔드 서버에서 인증 토큰을 검색하도록 지시합니다. 

1. [선택 사항입니다] 호출 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 확인할 수 있는 리소스를 확인합니다. 다음 `resources` 매개 변수는 사용자의 인증 토큰과 연결된 보호된 리소스의 배열입니다.\
   **트리거:** `preAuthorizedResources()` callback\
   **실행 지점:** 완료된 인증 흐름 후

1. 인증이 성공하면 인증 흐름을 진행합니다.

 

### D. 인증 흐름 {#authz_flow}

1. 호출 [`getAuthorization()`](#$getAuthZ) 인증 흐름을 시작합니다.

   종속성: 유효한 ResourceID가 MVPD와 동의됩니다.

   **참고:** ResourceID는 다른 장치나 플랫폼에서 사용되는 것과 동일해야 하며 MVPD에서 동일합니다.

1. 인증 및 권한 부여의 유효성을 검사합니다.

   - 만약 `getAuthorization()` 호출 성공: 사용자에게 유효한 AuthN 및 AuthZ 토큰이 있습니다(사용자가 인증되고 요청된 미디어를 볼 수 있는 권한이 있음).
   - If `getAuthorization()` 실패: throw된 예외를 검사하여 해당 유형(AuthN, AuthZ 등)을 확인합니다.
      - 인증(AuthN) 오류인 경우 인증 흐름을 다시 시작합니다.
      - 인증(AuthZ) 오류인 경우 사용자는 요청된 미디어를 볼 수 있는 권한이 없으며 일부 오류 메시지가 사용자에게 표시되어야 합니다.
      - 다른 유형의 오류(연결 오류, 네트워크 오류 등)가 있는 경우 그런 다음 사용자에게 적절한 오류 메시지를 표시합니다.

1. 짧은 미디어 토큰의 유효성을 검사합니다.

   Adobe Primetime 인증 미디어 토큰 확인 프로그램 라이브러리를 사용하여 `getAuthorization()` 위에 호출하십시오.

   - 유효성 검사가 성공하면: 사용자에 대해 요청된 미디어를 재생합니다.
   - 유효성 검사가 실패한 경우: AuthZ 토큰이 잘못되었습니다. 미디어 요청이 거부되어야 하며 오류 메시지가 사용자에게 표시되어야 합니다.

1. 일반 응용 프로그램 흐름으로 돌아갑니다.

### E. 미디어 흐름 보기 {#media_flow}

1. 사용자가 볼 미디어를 선택합니다.
1.  미디어가 보호됩니까?  선택한 미디어가 보호되어 있는지 애플리케이션에서 확인합니다.
   - 선택한 미디어를 보호하면 애플리케이션이 [인증 흐름](#authz_flow) 위에 표시됩니다.
   - 선택한 미디어가 보호되지 않은 경우 사용자를 위해 미디어를 재생합니다.

### F. 로그아웃 흐름 {#logout_flow}

1. 호출 [`logout()`](#$logout) 를 입력하여 사용자를 로그아웃합니다. \
   AccessEnabler는 Single Sign On을 통해 로그인을 공유하는 모든 요청에서 현재 MVPD에 대해 사용자가 얻은 캐시된 모든 값과 토큰을 지웁니다. 캐시를 지운 후 AccessEnabler는 서버 호출을 수행하여 서버측 세션을 정리합니다.  서버 호출로 인해 IdP로 SAML 리디렉션이 발생할 수 있으므로(IdP 측에서 세션 정리를 허용) 이 호출은 모든 리디렉션을 따라야 합니다. 이러한 이유로 이 호출은 사용자에게 보이지 않는 WebView 컨트롤 내에서 처리됩니다.

   **참고:** 로그아웃 흐름은 사용자가 어떤 식으로든 WebView와 상호 작용할 필요가 없다는 점에서 인증 흐름과 다릅니다. 따라서 WebView 컨트롤을 표시(즉, 숨김))을 클릭하여

