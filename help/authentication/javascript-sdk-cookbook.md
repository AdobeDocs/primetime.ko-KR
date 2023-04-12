---
title: JavaScript SDK Cookbook
description: JavaScript SDK Cookbook
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# JavaScript SDK Cookbook {#javascript-sdk-cookbook}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 소개(#intro)

이 문서에서는 Adobe Primetime 인증 서비스와 JavaScript 통합을 위해 Programmer의 상위 수준 응용 프로그램이 구현하는 자격 워크플로우를 설명합니다. JavaScript API 참조에 대한 링크는 전체에서 포함됩니다.

또한 [관련 정보](#related) 섹션에는 JavaScript 코드 샘플 세트에 대한 링크가 포함되어 있습니다.

## 자격 흐름(#entitlement)

1. [전제 조건](#prereq)
2. [시작 흐름](#startup)
3. [인증 흐름](#authn)
4. [인증 흐름](#authz)
5. [미디어 흐름 보기](#logout)

</br>

![](assets/javascript-flows.png)


## 사전 요구 사항(#prereq)

**종속성:**

- Adobe Primetime 인증 라이브러리(AccessEnabler)를 사용하려면 Adobe Primetime 인증 계정 관리자와 함께 이를 정렬합니다.
- 유효한 Adobe Primetime 인증 요청자Id인 경우, Adobe Primetime 인증 계정 관리자와 함께 이 항목을 배열하십시오.

콜백 함수를 만듭니다.

- `entitlementLoaded`

</br>

**트리거:** AccessEnabler가 로드되고 초기화를 마쳤습니다.

- `displayProviderDialog(mvpds)`

   **트리거:** `getAuthentication(),` 사용자가 공급자(MVPD)를 선택하지 않았고 아직 인증되지 않은 경우에만 mvpds 매개 변수는 사용자가 사용할 수 있는 공급자 배열입니다.

- `setAuthenticationStatus(status, errorcode)`

   **트리거:**
   - `checkAuthentication()`항상
   - `getAuthentication()` 사용자가 이미 인증되고 공급자를 선택한 경우에만 해당됩니다.

   반환된 상태는 성공 또는 실패입니다. errorcode는 오류 유형을 설명합니다.

- `createIFrame(width, height)`

   **트리거:** `setSelectedProvider(providerID)`선택한 공급자가 IFrame에 표시되도록 구성된 경우에만 해당됩니다.

   >[!NOTE]
   >
   >공급자는 인증 화면을 리디렉션 또는 iFrame으로 렌더링하도록 구성되며, 프로그래머는 둘 다 고려해야 합니다.

- `sendTrackingData(event, data)`

   **트리거:** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`.  다음 `event` 매개 변수는 자격 이벤트가 발생한 경우를 나타냅니다. a `data` 매개 변수는 이벤트와 관련된 값 목록입니다. 
- `setToken(token, resource)`

   **트리거:** `checkAuthorization()`및 `getAuthorization()` 리소스를 볼 수 있는 권한이 성공적으로 부여된 후.   다음 `token` 매개 변수는 단기 미디어 토큰입니다. a `resource` 매개 변수는 사용자가 볼 수 있는 권한이 있는 콘텐츠입니다.

- `tokenRequestFailed(resource, code, description)`

   **트리거:**`checkAuthorization()`&#x200B;및`getAuthorization()`  승인 실패 후.\
   다음 `resource` 매개 변수는 사용자가 보려고 하는 콘텐츠입니다. a `code` 매개 변수는 발생한 실패 유형을 나타내는 오류 코드입니다. a `description` 매개 변수는 오류 코드와 연관된 오류를 설명합니다.

- `selectedProvider(mvpd)`

   **트리거:** [`getSelectedProvider()`](#$getSelProv `mvpd` 매개 변수는 사용자가 선택한 공급자에 대한 정보를 제공합니다.

- `setMetadataStatus(metadata, key, arguments)`

   **트리거:** `getMetadata().`\
   다음 `metadata` 매개 변수는 요청한 특정 데이터를 제공합니다. key 매개 변수는 `getMetadata()`요청; 그리고 `arguments` 매개 변수는 에 전달된 것과 동일한 사전입니다 `getMetadata()`.


## 2. 시작 흐름

**I. AccessEnabler JavaScript를 로드합니다.**

**스테이징 프로필**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

또는..

**프로덕션 프로필의 경우**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

**트리거:** 초기화가 완료되면 Adobe Primetime 인증이 `entitlementLoaded()` 콜백 함수입니다. AccessEnabler와의 애플리케이션 커뮤니케이션의 시작 지점입니다. 

 
**내가..** 호출 `setRequestor()`프로그래머의 정체성을 확립하기 위해서 프로그래머에게 `requestorID` 및 (선택 사항) Adobe Primetime 인증 엔드포인트의 배열입니다.

**트리거:** 없음, 하지만 `displayProviderDialog()` 필요할 때 호출될 수 있습니다.


**3.** 호출 `checkAuthentication()` 전체 [인증 흐름].  이 호출이 성공하면 를 직접 진행할 수 있습니다. `authorization flow`.  그렇지 않은 경우 `authentication flow`.

**종속성:** 에 대한 성공적인 호출 `setRequestor()`(이 종속성은 모든 후속 호출에도 적용됩니다.)

 **트리거:** `setAuthenticationStatus()` callback

</br>

## 3. 인증 흐름</span>


**종속성:** 에 대한 성공적인 호출 `setRequestor()`(이 종속성은 모든 후속 호출에도 적용됩니다.)


호출 `getAuthentication()` 인증 상태를 가져오거나 공급자 인증 흐름을 트리거하려면

**트리거:**

- `displayProviderDialog()`사용자가 아직 인증되지 않은 경우
- `setAuthenticationStatus()` 인증이 이미 수행된 경우

AccessEnabler가 호출되면 인증 흐름이 완료됩니다 `setAuthenticationStatus()`with `isAuthenticated == 1`.

## 4. 허가흐름(#authz)

**종속성:**

- 에 대한 성공적인 호출 `setRequestor()` (이 종속성은 모든 후속 호출에도 적용됩니다.)
- 유효한 ResourceID가 MVPD와 동의됩니다. ResourceID는 다른 장치나 플랫폼에서 사용되는 것과 동일해야 하며 MVPD에서 동일하게 됩니다.

호출 `getAuthorization()` 요청된 미디어에 대한 ResourceID를 전달합니다. 성공적으로 호출되면 짧은 미디어 토큰이 반환됩니다. 그러면 사용자가 요청된 미디어를 볼 수 있음을 확인할 수 있습니다.

- 호출이 전달되는 경우: 사용자에게 유효한 AuthN 토큰이 있으며 사용자가 요청된 미디어를 볼 수 있는 권한이 있습니다.
- 호출이 실패하면: throw된 예외를 검사하여 해당 유형(AuthN, AuthZ 등)을 확인합니다.
- 호출이 AuthN 오류인 경우 AuthN 플로우를 다시 시작합니다.
- 호출이 AuthZ 오류인 경우 사용자가 요청된 미디어를 볼 수 있는 권한이 없으며 일부 유형의 오류 메시지가 사용자에게 표시되어야 합니다.
- 다른 오류(연결 오류, 네트워크 오류 등)가 발생한 경우 그런 다음 사용자에게 적절한 오류 메시지를 표시합니다.

성공적으로 반환된 shortMediaToken의 유효성을 검사하려면 미디어 토큰 확인 도구를 사용하십시오 `getAuthorization()` 호출.

 
**종속성:** Short Media 토큰 확인기(AccessEnabler 라이브러리에 포함됨)

- 유효성 검사가 전달되는 경우: 사용자에 대해 요청된 미디어를 표시/재생합니다.
- 실패한 경우: AuthZ 토큰이 잘못되었습니다. 미디어 요청이 거부되어야 하며 오류 메시지가 사용자에게 표시되어야 합니다.

## 5. 미디어 흐름 보기(#logout)

- 사용자가 볼 미디어를 선택합니다.
   - 미디어가 보호됩니까?\
          - 앱이 미디어가 보호되어 있는지 확인합니다.
      - 미디어가 보호된 경우 앱은 위의 인증(AuthZ) 플로우를 시작합니다.
      - 미디어가 보호되지 않은 경우 미디어 보기 플로우를 계속 진행합니다.
      - 재생 미디어

## 방문자 ID 구성(#visitorID)

구성 [Experience Cloud visitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) analytics POV에서는 값이 매우 중요합니다. EC visitorID 값이 설정되면 SDK는 모든 네트워크 호출과 함께 이 정보를 전송하고 Adobe Primetime 인증 서비스가 이 정보를 수집합니다. 이 방법으로 Adobe Primetime 인증 서비스의 분석 데이터를 다른 애플리케이션 또는 웹 사이트에서 보유할 수 있는 다른 분석 보고서와 상호 연관시킬 수 있습니다. EC visitorID 설정 방법에 대한 정보를 찾을 수 있습니다 [여기](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en).

 
>[!NOTE]
>
>이 기능 지원은 JS SDK 버전 3.1.0부터 사용할 수 있습니다. 

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->