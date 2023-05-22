---
title: JavaScript SDK API 참조
description: JavaScript SDK API 참조
exl-id: 48d48327-14e6-46f3-9e80-557f161acd8a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---

# JavaScript SDK API 참조 {#javascript-sdk-api-reference}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 허가되지 않은 사용은 허용되지 않습니다.

## API 참조 {#api-reference}

이러한 기능은 MVPD와의 상호 작용 요청을 시작합니다. 모든 호출은 비동기적이므로 [콜백](#callbacks) 응답을 처리하려면:

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor (inRequestorID, endpoints, options){#setrequestor(inRequestorID,endpoints,options)}

**설명:** 요청이 시작되는 사이트를 식별합니다.  통신 세션에서 다른 API 호출 전에 이 호출을 수행해야 합니다. 

**매개 변수:**

- *inRequestorID* - Adobe이 등록 중에 원래 사이트에 할당한 고유 식별자입니다.

- *엔드포인트* - 이 매개 변수는 선택 사항입니다. 다음 값 중 하나일 수 있습니다.

   - Adobe에서 제공하는 인증 및 권한 부여 서비스의 끝점을 지정할 수 있는 배열입니다(디버깅 목적으로 다른 인스턴스를 사용할 수 있음). 여러 개의 URL이 제공되는 경우, MVPD 목록은 모든 서비스 제공자의 엔드포인트로 구성된다. 각 MVPD는 가장 빠른 서비스 공급자, 즉 먼저 응답하고 해당 MVPD를 지원하는 공급자와 연결됩니다. 기본적으로(값을 지정하지 않으면) Adobe 서비스 공급자가 사용됩니다(<http://sp.auth.adobe.com/>).

   예:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *옵션* - 애플리케이션 ID 값, 방문자 ID 값 새로 고침 불가 설정(백그라운드 로그인 로그아웃) 및 MVPD 설정(iFrame)이 포함된 JSON 개체입니다. 모든 값은 선택 사항입니다.
   1. 지정하면 라이브러리에서 수행한 모든 네트워크 호출에 대해 Experience Cloud visitorID가 보고됩니다. 이 값은 나중에 고급 분석 보고서에 사용할 수 있습니다.
   2. 애플리케이션의 고유 식별자가 지정된 경우 -`applicationId` - 이 값은 X-Device-Info HTTP 헤더의 일부로 응용 프로그램에서 수행한 모든 후속 호출에 추가됩니다. 이 값은 나중에 가져올 수 있습니다. [ESM](/help/authentication/entitlement-service-monitoring-overview.md) 적절한 쿼리를 사용하여 보고합니다.

   **참고:** 모든 JSON 키는 대/소문자를 구분합니다.

    예:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- 프로그래머는 로그인에 iFrame이 필요한지 여부를 지정하여 Adobe Primetime 인증에 구성된 MVPD 설정을 재정의할 수 있습니다(*iFrameRequired* 키) 및 iFrame 차원(*iFrame 너비* 및 *iFrameHeight* 키). JSON 개체에는 다음 템플릿이 있습니다.

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```
 

위의 템플릿에 있는 모든 최상위 키는 선택 사항이며, 기본값(*backgroundLog*, *backgroundLogut*&#x200B;은 기본적으로 false이고 mvpdConfig는 null입니다. 즉, MVPD 설정이 재정의되지 않습니다.

 
- **참고**: 위의 매개 변수에 잘못된 값/유형을 지정하면 정의되지 않은 동작이 발생합니다.

 

다음은 새로 고침 없는 로그인 및 로그아웃을 활성화하고, MVPD1을 전체 페이지 리디렉션 로그인(iFrame 아님)으로 변경하고, MVPD2를 iFrame으로 로그인하여 너비=500 및 높이=300인 시나리오에 대한 예제 구성입니다.

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**트리거된 콜백:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[맨 위로 돌아가기](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**설명:** 지정된 리소스에 대한 권한 부여를 요청합니다. 고객이 승인 가능 리소스에 액세스할 때마다 이 함수를 호출하여 Access Enabler에서 단기 인증 토큰을 얻습니다. 리소스 ID는 인증을 제공하는 MVPD와 동의합니다.

현재 고객에 대해 캐시된 인증 토큰을 사용합니다. 해당 토큰이 없으면 먼저 인증 프로세스를 시작한 다음 권한 부여를 계속합니다.\
 
**매개 변수:**

- `inResourceID` - 사용자가 권한 부여를 요청하는 리소스의 ID입니다.
- `redirect_url` - 선택적으로 MVPD의 인증 프로세스가 인증을 시작한 페이지가 아닌 해당 페이지로 사용자를 반환하도록 리디렉션 URL을 제공합니다.


**트리거된 콜백:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) 성공 시, [token요청 실패](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) 실패 시

>[!CAUTION]
>
>가능하면 getAuthorization() 대신 checkAuthorization()을 사용하십시오. getAuthorization() 메서드는 전체 인증 흐름을 시작하며(사용자가 인증되지 않은 경우) 이로 인해 프로그래머측의 구현이 복잡해질 수 있습니다.

</b>

[맨 위로 돌아가기](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**설명:** 현재 고객에 대한 인증을 요청합니다. 일반적으로 로그인 단추 클릭에 따라 호출됩니다. 현재 고객에 대해 캐시된 인증 토큰을 확인합니다. 해당 토큰이 없으면 가 인증 프로세스를 시작합니다. 기본 또는 사용자 지정 공급자 선택 대화 상자를 호출한 다음 선택한 공급자를 사용하여 MVPD의 로그인 인터페이스로 리디렉션합니다.

성공 시 는 사용자에 대한 인증 토큰을 만들고 저장합니다. 인증에 실패하면 공급자가 적절한 오류 메시지를 [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) callback.

**매개 변수:**

- redirect_url - 선택적으로 MVPD의 인증 프로세스가 인증을 시작한 페이지가 아닌 해당 페이지로 사용자를 반환하도록 리디렉션 URL을 제공합니다.

 **트리거된 콜백:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[맨 위로 돌아가기](#top)

</br>

## checkAuthN {#checkauthn}

**설명:** 현재 고객의 현재 인증 상태를 확인합니다.  UI와 연결되어 있지 않습니다.

**트리거된 콜백:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[맨 위로 돌아가기](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**설명:** 이 방법은 애플리케이션에서 현재 고객 및 지정된 리소스에 대한 인증 상태를 확인하는 데 사용됩니다. 먼저 인증 상태를 확인하는 것으로 시작됩니다. 인증되지 않은 경우 tokenRequestFailed() 콜백이 트리거되고 메서드가 종료됩니다. 사용자가 인증되면 권한 부여 플로우도 트리거됩니다. 다음에서 세부 사항 보기 [getAuthorization()](#getAuthZ 메서드.

>[!TIP]
>
> **확인 상태 함수 사용**  권한 부여를 요청하기 전에 인증 또는 권한 부여 상태를 확인할 필요가 없습니다. 예를 들어 이러한 함수를 호출하여 자신의 상태 표시를 업데이트할 수 있습니다. 사용자 상호 작용이 필요한 경우 사용하지 마십시오.

**매개 변수:**

- `inResourceID` - 사용자가 권한 부여를 요청하는 리소스의 ID입니다.

 
**트리거된 콜백:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**설명:** 리소스 목록에 대한 &quot;preflight&quot; 인증 상태를 요청합니다.

**매개 변수:**

- *리소스*: resources 매개 변수는 권한 부여를 확인해야 하는 리소스 배열입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 의 리소스 ID와 동일한 제한이 적용됩니다. `getAuthorization()` 즉, 프로그래머와 MVPD 간에 설정된 합의된 값 또는 미디어 RSS 조각입니다. 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

이 API 변형은 JS SDK 버전 4.0부터 사용할 수 있습니다


**매개 변수:**

- *리소스*: resources 매개 변수는 권한 부여를 확인해야 하는 리소스 배열입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 의 리소스 ID와 동일한 제한이 적용됩니다. `getAuthorization()` 즉, 프로그래머와 MVPD 간에 설정된 합의된 값 또는 미디어 RSS 조각입니다. 

- *캐시*: 사전 승인된 리소스를 확인할 때 내부 캐시를 사용할지 여부. 이는 선택적 매개 변수이며 기본값은 입니다. **true**. true인 경우 동작은 위의 API와 동일합니다. 즉, 이 함수에 대한 후속 호출은 내부 캐시를 사용하여 사전 승인된 리소스를 확인합니다. 통과 **false** 이 매개변수에 대해 내부 캐시가 비활성화되므로 **checkPreauthorizedResources** API가 호출됩니다.

**트리거된 콜백:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[맨 위로 돌아가기](#top)
</br>

## getMetadata(키) {#getMetadata}

**설명:** Access Enabler 라이브러리에서 메타데이터로 노출된 정보를 검색합니다.

메타데이터에는 두 가지 유형이 있습니다. 

- **정적** (인증 토큰 TTL, 인증 토큰 TTL 및 장치 ID) 
- **사용자 메타데이터** (여기에는 인증 및/또는 인증 흐름 동안 MVPD에서 사용자의 장치로 전달되는 사용자 특정 정보가 포함됩니다.)

**추가 정보:** [사용자 메타데이터](#UserMetadata)

**매개 변수:**

- *key*: 요청한 메타데이터를 지정하는 ID:
   - 키가 `"TTL_AUTHN",` 그런 다음 인증 토큰 만료 시간을 얻기 위해 쿼리가 수행됩니다.

   - 키가 `"TTL_AUTHZ"` 및 params는 리소스 id를 문자열로 포함하는 배열입니다. 그런 다음 쿼리를 수행하여 지정된 리소스와 연결된 인증 토큰의 만료 시간을 구합니다.

   - 키가 `"DEVICEID"` 그런 다음 현재 장치 id를 얻기 위해 쿼리가 수행됩니다. 이 기능은 기본적으로 비활성화되어 있으며 프로그래머는 사용 권한 및 요금에 대한 정보를 Adobe에 문의해야 합니다.

   - 키가 다음 사용자 메타데이터 유형 목록에서 가져온 경우 해당 사용자 메타데이터가 포함된 JSON 개체가으로 전송됩니다. [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) callback 함수:

   - `"zip"` - 우편 번호

   - `"encryptedZip"` - 암호화된 우편 번호

   - `"householdID"` - 세대 식별자. MVPD가 하위 계정을 지원하지 않는 경우에는 이 값이 userID와 동일합니다.

   - `"maxRating"` - 사용자의 최대 자녀 보호 등급

   - `"userID"` - 사용자 식별자. MVPD가 하위 계정을 지원하고 사용자가 주 계정이 아닌 경우 userID는 householdID와 다릅니다.

   - `"channelID"` - 사용자가 볼 수 있는 채널 목록

   - `"is_hoh"` - 사용자가 세대주인지 여부를 식별하는 플래그

   - `"encryptedZip"` - 암호화된 우편 번호

   - `"typeID"` - 사용자 계정이 기본/보조 계정인지 식별하는 플래그입니다.

   - `"primaryOID"` - 세대 식별자

   - `"postalCode"` - 우편 번호와 유사

   - `"acctID"` - 계정 ID

   - `"acctParentID"` - 계정 상위 ID
   **참고**: 프로그래머가 사용할 수 있는 실제 사용자 메타데이터는 MVPD가 제공하는 기능에 따라 다릅니다.  다음을 참조하십시오 [사용자 메타데이터](#UserMetadata) 사용 가능한 사용자 메타데이터의 현재 목록입니다.


예:

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```
 

**트리거된 콜백:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[맨 위로 돌아가기](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**설명:** 사용자가 공급자 선택 UI에서 공급자 선택을 Access Enabler로 보내기 위해 MVPD를 선택한 경우 이 함수를 호출하거나 사용자가 공급자를 선택하지 않고 공급자 선택 UI를 해제한 경우 null 매개 변수를 사용하여 이 함수를 호출합니다. 

**트리거된 콜백:**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[맨 위로 돌아가기](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**설명:** 공급자 선택 대화 상자에서 고객의 선택 결과를 검색합니다. 초기 인증 확인 후 언제든지 사용할 수 있습니다.

이 함수는 비동기적으로 작동하며 결과를 `selectedProvider()` callback 함수.

- **MVPD** 현재 선택한 MVPD이거나 MVPD가 선택되지 않은 경우 null입니다.
- **AE_State** 현재 고객에 대한 &quot;새 사용자&quot;, &quot;사용자가 인증되지 않음&quot; 또는 &quot;사용자가 인증됨&quot; 중 하나의 인증 결과

 **트리거된 콜백:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[맨 위로 돌아가기](#top)

</br>

## 로그아웃 {#logout}

**설명:** 현재 고객을 로그아웃하여 해당 사용자에 대한 모든 인증 및 권한 부여 정보를 지웁니다. 고객 시스템에서 모든 authN 및 authZ 토큰을 삭제합니다.

 **트리거된 콜백:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[맨 위로 돌아가기](#top)

</br>

## 콜백 정의 {#calllback-definitions}

비동기 요청 호출에 대한 응답을 처리하려면 다음 콜백을 구현해야 합니다.

- [entitlementLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## entitlementLoaded() {#entitlementLoaded}

**설명:** Access Enabler가 초기화를 완료하고 요청을 받을 준비가 되면 트리거됩니다. 이 콜백을 구현하여 Access Enabler API와의 통신을 시작할 수 있는 시기를 알 수 있습니다.
</br>

[위로 돌아가기](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**설명:** 구성 정보 및 MVPD 목록을 받으려면 이 콜백을 구현하십시오.

**매개 변수:**

- *configXML*: MVPD 목록을 포함하는 현재 요청자의 구성을 포함하는 xml 개체입니다.

 
**트리거 기준:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[위로 돌아가기](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**설명:** 이 콜백을 구현하여 사용자 지정 공급자 선택 UI를 호출합니다. 대화 상자에서 디스플레이 이름(및 로고(선택 사항))을 사용하여 고객이 선택할 수 있는 사항을 제공해야 합니다. 고객이 선택을 하고 대화 상자를 닫으면 호출에서 선택한 공급자에 대한 관련 ID를 로 보냅니다. *setSelectedProvider()*.

**매개 변수:**

- *공급자* - 요청된 MVPD를 나타내는 개체 배열:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**트리거 기준:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[위로 돌아가기](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**설명:** 사용자가 인증 로그인 페이지 UI를 표시할 iFrame이 필요한 MVPD를 선택한 경우 이 콜백을 구현합니다.

**트리거 기준:**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [위로 돌아가기](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**설명:** 인증 상태(검사를 성공적으로 완료하면 빈 문자열)를 확인하는 동안 오류가 발생한 경우 인증 상태(1=인증됨 또는 0=인증되지 않음) 및 설명 오류 메시지를 받도록 이 콜백을 구현합니다.

>[!NOTE]
> 
>현재를 사용하는 경우 [고급 오류 보고](/help/authentication/error-reporting.md) 시스템에서는 이 함수로 전송된 errorCode 매개 변수를 무시할 수 있습니다.  하지만 isAuthenticated 플래그는 자격 흐름에서 사용자의 인증 상태를 추적하는 데 여전히 사용됩니다


**매개 변수:**

- *isAuthenticated* - 인증 상태를 제공합니다(1(인증됨) 또는 0(인증되지 않음)).
- *errorCode* - 인증 상태를 확인할 때 발생한 모든 오류. 없는 경우 빈 문자열.

 
**트리거 기준:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[위로 돌아가기](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>장치 유형 및 운영 체제는 공개 Java 라이브러리 ( )를 사용하여 파생됩니다.<http://java.net/projects/user-agent-utils>)와 사용자 에이전트 문자열. 이 정보는 운영 지표를 장치 범주로 분류하는 거친 방법으로만 제공되지만, 잘못된 결과에 대해서는 Adobe이 책임을 지지 않을 수 있습니다. 그에 따라 새로운 기능을 사용하십시오.

**설명:** 특정 이벤트가 발생할 때 추적 데이터를 받으려면 이 콜백을 구현합니다. 예를 들어 동일한 자격 증명으로 로그인한 사용자가 몇 명인지 추적할 수 있습니다. 추적은 현재 구성할 수 없습니다. Adobe Primetime 인증 1.6 사용, `sendTrackingData()` 디바이스, Access Enabler 클라이언트 및 운영 체제 유형에 대한 정보도 보고합니다. 다음 `sendTrackingData()` 콜백은 이전 버전과 호환됩니다.\
 
- 장치 유형에 가능한 값:
   - 컴퓨터
   - 태블릿
   - 모바일
   - 가메콘솔
   - 알 수 없음

- Access Enabler 클라이언트 유형에 사용할 수 있는 값은 다음과 같습니다.
   - html5
   - ios
   - android


이벤트 유형 및 관련 정보 배열을 전달합니다. 이벤트 유형은 다음과 같습니다.

| mvpdSelection | 사용자가 공급자 선택 대화 상자에서 MVPD를 선택했습니다. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDiscovery | 인증 확인이 완료되었습니다. |
| authorizationDetection | 인증 요청이 완료되었습니다. |

</br>
데이터는 각 이벤트 유형에 따라 다릅니다.
</br>

| 이벤트 유형(문자열) | 데이터(배열) |
|:--- | :--- |
| mvpdSelection | 0: 선택한 MVPD |
|  | 1: 장치 유형 |
|  | 2: Access Enabler 클라이언트 유형 |
|  | 3: OS |
| authenticationDiscovery | 0: 토큰 요청의 성공 여부(true/false) |
|  | 1: MVPD ID |
|  | 2: GUID |
|  | 3: 토큰이 캐시에 이미 있습니다(true/false). |
|  | 4: 장치 유형 |
|  | 5: Access Enabler 클라이언트 유형 |
|  | 6: OS |
| authorizationDetection | 0: 토큰 요청의 성공 여부(true/false) |
|  | 1: MVPD ID |
|  | 2: GUID |
|  | 3: 토큰이 캐시에 이미 있습니다(true/false). |
|  | 4: 오류 |
|  | 5: 세부 정보 |
|  | 6: 장치 유형 |
|  | 7: Access Enabler 클라이언트 유형 |
|  | 8: OS |


**트리거 기준:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[위로 돌아가기](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**설명:** 이 콜백을 구현하여 권한 부여 요청 또는 검사 권한 부여가 완료되고 성공적으로 완료된 단기 미디어 토큰(inToken)과 리소스의 ID(inRequestedResourceID)를 받습니다.

**트리거 기준:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[위로 돌아가기](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**설명:** 권한 부여 또는 검사 권한 부여 요청이 실패했을 때 신호를 받으려면 이 콜백을 구현합니다. 프로그래머가 표시할 사용자 지정 메시지를 제공하기 위해 MVPD가 선택적으로 사용할 수 있습니다.

>[!IMPORTANT]
>
>이 콜백 함수는 이전의 원래 Primetime 인증 오류 보고 시스템의 일부입니다. 이전 버전과의 호환성을 위해 유지되지만 현재 고급 오류 보고 시스템을 사용하여 자체 콜백을 구현한 경우에는 이 함수를 전혀 사용할 필요가 없습니다. 최신 오류 보고 시스템에서는 각 유형의 오류 또는 경고에 대해 권장되는 작업 과정과 함께 인증(또는 기타 작업)이 실패한 이유에 대한 자세한 정보를 제공합니다.

**매개 변수:**

- *inRequestedResourceID* - 권한 부여 요청에 사용된 리소스 ID를 제공하는 문자열입니다.
- *inRequestErrorCode* - 실패 이유를 나타내는 Adobe Primetime 인증 오류 코드를 표시하는 문자열. 가능한 값은 &quot;사용자가 인증되지 않음 오류&quot; 및 &quot;사용자가 인증되지 않음 오류&quot;입니다. 자세한 내용은 아래 &quot;콜백 오류 코드&quot;를 참조하십시오.
- *inRequestDetailedErrorMessage* - 표시에 적합한 추가 설명 문자열. 어떤 이유로든 이 설명 문자열을 사용할 수 없는 경우 Adobe Primetime 인증에서 빈 문자열을 보냅니다 **(&quot;&quot;)**.  이는 MVPD가 사용자 지정 오류 메시지 또는 판매 관련 메시지를 전달하는 데 사용할 수 있습니다. 예를 들어, 가입자가 리소스에 대한 승인이 거부되면 MVPD는 `*inRequestDetailedErrorMessage*` 예: **&quot;현재 패키지에서 이 채널에 액세스할 수 없습니다. 패키지를 업그레이드하려면 \*여기\*를 클릭하십시오.&quot;** 이 콜백을 통해 Adobe Primetime 인증을 통해 프로그래머 사이트로 메시지가 전달됩니다. 그러면 프로그래머는 이를 표시하거나 무시할 수 있는 옵션이 있습니다. Adobe Primetime 인증은 다음을 사용할 수도 있습니다 `*inRequestDetailedErrorMessage*` 을 클릭하여 프로그래머에게 오류가 발생했을 수 있는 조건을 알립니다. 예를 들어, **&quot;공급자의 인증 서비스와 통신하는 동안 네트워크 오류가 발생했습니다.&quot;**

 

**트리거 기준:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[위로 돌아가기](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**설명:** 호출 후에 반환되는 승인된 리소스 목록을 제공하는 Access Enabler에 의해 트리거된 콜백입니다. `checkPreauthorizedResources()`.

**매개 변수:**

- *authorizedSources*: 승인된 리소스의 목록입니다.

**트리거 기준:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[위로 돌아가기](#top)

</br>

## setMetadataStatus(키, 암호화, 데이터) {#setMetadataStatus(key,encrypted,data)}

**설명:** 다음을 통해 요청된 메타데이터를 전달하는 Access Enabler에 의해 트리거된 콜백 `getMetadata()` 호출합니다.

**추가 정보:** [사용자 메타데이터](#userMetadata)

**매개 변수:**

- *키(문자열)*: 요청을 수행한 메타데이터의 키입니다.
- *암호화됨(부울)*: &quot;value&quot;의 암호화 여부를 나타내는 플래그입니다. &quot;true&quot;이면 &quot;value&quot;는 실제로 실제 값의 JSON 웹 암호화 표현입니다. 
- *데이터(JSON 개체)*: 메타데이터가 표시된 JSON 개체입니다. 단순 요청의 경우(&#39;)`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;), 결과는 문자열(인증 TTL, 권한 부여 TTL 또는 장치 ID를 나타냄)입니다. 사용자 메타데이터 요청의 경우 결과는 메타데이터 페이로드를 나타내는 프리미티브 또는 JSON 개체일 수 있습니다. JSON 사용자 메타데이터 개체의 실제 구조는 다음과 유사합니다.

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```
 

예:

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```
 

**트리거 기준:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[위로 돌아가기](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**설명:** 이 콜백을 구현하여 현재 선택된 MVPD와(과) 함께 래핑된 현재 사용자의 인증 결과를 받습니다. `result` 매개 변수. 다음 `result` 매개 변수는 다음 속성을 가진 개체입니다.

- **MVPD** 현재 선택한 MVPD이거나 MVPD가 선택되지 않은 경우 null입니다.
- **AE\_State** 현재 사용자에 대한 인증 결과, &quot;새 사용자&quot;, &quot;사용자가 인증되지 않음&quot; 또는 &quot;사용자가 인증됨&quot; 중 하나

 **트리거 기준:** [getSelectedProvider()](#getSelProv)

</br>

[위로 돌아가기](#top)

</br>

### 콜백 오류 코드 {#callback-error-codes}

| 일반 오류 |  |
|:--- | :--- | 
| 내부 오류 | 요청을 처리하는 동안 시스템 오류가 발생했습니다. |
| 공급자가 선택되지 않음 오류 | 고객이 공급자 선택 대화 상자에서 취소할 때 발생합니다. |
| 공급자를 사용할 수 없음 오류 | 사용할 수 있는 공급자가 없을 때 발생합니다. |

| 인증 오류 |  |
|:--- | :--- | 
| 일반 인증 오류 | 이유를 알 수 없거나 게시할 수 없을 때 반환됩니다. |
| 내부 인증 오류 | 인증을 시도하는 동안 시스템 오류가 발생했습니다. |
| 사용자가 인증되지 않음 오류 | 사용자가 인증되지 않았습니다. |
| 다중 인증 요청 오류 | 추가 인증 요청은 첫 번째 요청이 완료되기 전에 수신되었습니다. |

| 인증 오류 |  |
|:--- | :--- | 
| 일반 인증 오류 | 이유를 알 수 없거나 게시할 수 없을 때 반환됩니다. |
| 내부 인증 오류 | 권한을 부여하는 동안 시스템 오류가 발생했습니다. |
| 사용자가 승인되지 않음 오류 | 고객은 요청된 콘텐츠를 볼 수 있는 권한이 없습니다. |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[맨 위로 돌아가기](#top)
