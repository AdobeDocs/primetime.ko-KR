---
title: JavaScript SDK API 참조
description: JavaScript SDK API 참조
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# JavaScript SDK API 참조 {#javascript-sdk-api-reference}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## API 참조 {#api-reference}

이러한 함수는 MVPD와의 상호 작용을 요청합니다. 모든 호출은 비동기적입니다. 를 구현해야 합니다. [콜백](#callbacks) 응답을 처리하려면

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor(inRequestorID, 끝점, 옵션){#setrequestor(inRequestorID,endpoints,options)}

**설명:** 요청이 시작되는 사이트를 식별합니다.  통신 세션에서 다른 API 호출 전에 이 호출을 수행해야 합니다. 

**매개 변수:**

- *inRequestorID* - Adobe이 등록 중에 원래 사이트에 할당된 고유 식별자입니다.

- *끝점* - 이 매개 변수는 선택 사항입니다. 다음 값 중 하나일 수 있습니다.

   - Adobe이 제공하는 인증 및 인증 서비스의 끝점을 지정할 수 있는 배열입니다(다른 인스턴스는 디버깅 용도로 사용될 수 있음). 여러 URL이 제공되는 경우 MVPD 목록은 모든 서비스 공급자의 끝점으로 구성됩니다. 각 MVPD는 가장 빠른 서비스 공급자와 연결됩니다. 즉, 먼저 응답하고 해당 MVPD를 지원하는 공급자입니다. 기본적으로 (값이 지정되지 않은 경우) Adobe 서비스 공급자가 사용됩니다(<http://sp.auth.adobe.com/>).

   예:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *옵션* - 애플리케이션 ID 값, 방문자 ID 값 새로 고침 없는 설정(백그라운드 로그인 로그아웃) 및 MVPD 설정(iFrame)이 포함된 JSON 개체. 모든 값은 선택 사항입니다.
   1. 지정하면, Experience Cloud visitorID가 라이브러리에서 수행한 모든 네트워크 호출에 보고됩니다. 이 값은 나중에 고급 분석 보고서에 사용할 수 있습니다.
   2. 응용 프로그램의 고유 식별자를 지정한 경우 -`applicationId` - 값이 X-Device-Info HTTP 헤더의 일부로 애플리케이션에서 수행하는 모든 후속 호출에 추가됩니다. 이 값은 나중에 [ESM](/help/authentication/entitlement-service-monitoring-overview.md) 적절한 쿼리를 사용하는 보고서.

   **참고:** 모든 JSON 키는 대/소문자를 구분합니다.

    예:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- 프로그래머는 로그인(*iFrameRequired* key)와 iFrame 차원(*iFrameWidth* 및 *iFrameHeight* 키). JSON 개체에는 다음 템플릿이 있습니다.

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
 

위의 템플릿에 있는 모든 최상위 수준의 키는 선택 사항이며 기본값( )이 있습니다.*backgroundLogin*, *backgroundLogut*&#x200B;기본적으로 false이고 mvpdConfig가 null입니다. 즉, MVPD 설정이 오버라이드되지 않습니다.

 
- **참고**: 위의 매개 변수에 잘못된 값/유형을 지정하면 정의되지 않은 동작이 발생합니다.

 

다음은 다음 시나리오에 대한 구성 예입니다. 새로 고침이 없는 로그인 및 로그아웃을 활성화하고, MVPD1을 전체 페이지 리디렉션 로그인(iFrame 아님)으로 변경하고, MVPD2를 width=500 및 height=300으로 iFrame 로그인으로 변경합니다.

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


**콜백이 트리거됨:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[맨 위로 돌아가기](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**설명:** 지정된 리소스에 대한 권한 부여를 요청합니다. 고객이 승인 가능한 리소스에 액세스하려고 할 때마다 이 함수를 호출하여 Access Enabler에서 단기 인증 토큰을 얻습니다. 리소스 ID는 MVPD가 인증을 제공하는 데 동의됩니다.

현재 고객에 대해 캐시된 인증 토큰을 사용합니다. 이러한 토큰이 없으면 먼저 인증 프로세스를 시작한 다음 인증을 계속합니다.\
 
**매개 변수:**

- `inResourceID` - 사용자가 인증을 요청하는 리소스의 ID입니다.
- `redirect_url` - 선택적으로 리디렉션 URL을 제공하여 MVPD의 인증 프로세스가 권한이 시작된 페이지가 아닌 해당 페이지로 사용자를 돌아오도록 합니다.


**콜백이 트리거됨:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) 성공 [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) 실패 시

>[!CAUTION]
>
>가능하면 getAuthorization() 대신 checkAuthorization()을 사용하십시오. getAuthorization() 메서드는 전체 인증 흐름을 시작하고(사용자가 인증되지 않은 경우) 이로 인해 프로그래머 측에서 복잡한 구현이 발생할 수 있습니다.

</b>

[맨 위로 돌아가기](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**설명:** 현재 고객에 대한 인증을 요청합니다. 일반적으로 로그인 단추를 클릭하면 호출됩니다. 현재 고객에 대해 캐시된 인증 토큰을 확인합니다. 이러한 토큰이 없으면 인증 프로세스가 시작됩니다. 이 호출은 기본 또는 사용자 지정 공급자 선택 대화 상자를 호출한 다음 선택한 공급자를 사용하여 MVPD의 로그인 인터페이스로 리디렉션합니다.

성공하면 사용자에 대한 인증 토큰을 만들고 저장합니다. 인증이 실패하면 공급자가 [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) 콜백입니다.

**매개 변수:**

- redirect_url - 선택적으로 리디렉션 URL을 제공하여 MVPD의 인증 프로세스가 인증이 시작된 페이지가 아닌 해당 페이지로 사용자를 돌아오도록 합니다.

 **콜백이 트리거됨:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[맨 위로 돌아가기](#top)

</br>

## checkAuthN {#checkauthn}

**설명:** 현재 고객에 대한 현재 인증 상태를 확인합니다.  UI와 연결되지 않았습니다.

**콜백이 트리거됨:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[맨 위로 돌아가기](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**설명:** 이 방법은 응용 프로그램에서 현재 고객 및 해당 리소스에 대한 인증 상태를 확인하는 데 사용됩니다. 먼저 인증 상태를 확인하여 시작됩니다. 인증되지 않은 경우 tokenRequestFailed() 콜백이 트리거되고 메서드가 종료됩니다. 사용자가 인증되면 인증 흐름도 트리거됩니다. 자세한 내용은 [getAuthorization()]#getAuthZ 메서드를 사용합니다.

>[!TIP]
>
> **확인 상태 함수 사용**  인증을 요청하기 전에 인증 또는 권한 부여 상태를 확인할 필요가 없습니다. 예를 들어 이러한 함수를 호출하여 상태 표시를 업데이트할 수 있습니다. 사용자 상호 작용이 필요한 경우에는 사용하지 마십시오.

**매개 변수:**

- `inResourceID` - 사용자가 인증을 요청하는 리소스의 ID입니다.

 
**콜백이 트리거됨:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**설명:** 리소스 목록에 대해 &quot;프리플라이트&quot; 인증 상태를 요청합니다.

**매개 변수:**

- *리소스*: Resources 매개 변수는 인증을 확인해야 하는 리소스의 배열입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 `getAuthorization()` 즉, 프로그래머와 MVPD 또는 미디어 RSS 조각 간에 설정된 합의된 값입니다. 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

이 API 변형은 JS SDK 버전 4.0부터 사용할 수 있습니다


**매개 변수:**

- *리소스*: Resources 매개 변수는 인증을 확인해야 하는 리소스의 배열입니다. 목록의 각 요소는 리소스 ID를 나타내는 문자열이어야 합니다. 리소스 ID에는 `getAuthorization()` 즉, 프로그래머와 MVPD 또는 미디어 RSS 조각 간에 설정된 합의된 값입니다. 

- *캐시*: 사전 승인된 리소스를 확인할 때 내부 캐시를 사용할지 여부를 확인합니다. 선택적 매개변수이며 기본값 설정 **true**. true인 경우 동작은 위의 API와 동일하며, 이것은 이 함수에 대한 후속 호출에서 사전 승인된 리소스를 해결하기 위해 내부 캐시를 사용합니다. 전달 **false** 이 매개 변수에 대해 내부 캐시가 비활성화되어 **checkPreauthorizedResources** API를 호출합니다.

**콜백이 트리거됨:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[맨 위로 돌아가기](#top)
</br>

## getMetadata(Key) {#getMetadata}

**설명:** Access Enabler 라이브러리에서 메타데이터로 노출된 정보를 검색합니다.

메타데이터에는 두 가지 유형이 있습니다. 

- **정적** (인증 토큰 TTL, 인증 토큰 TTL 및 장치 ID) 
- **사용자 메타데이터** (여기에는 인증 및/또는 인증 흐름 중에 MVPD에서 사용자 장치로 전달되는 사용자 특정 정보가 포함됩니다.)

**추가 정보:** [사용자 메타데이터](#UserMetadata)

**매개 변수:**

- *key*: 요청된 메타데이터를 지정하는 ID입니다.
   - 키가 `"TTL_AUTHN",` 그런 다음 인증 토큰 만료 시간을 얻기 위해 쿼리가 수행됩니다.

   - 키가 `"TTL_AUTHZ"` 및 params 는 리소스 id를 문자열로 포함하는 배열로, 지정한 리소스와 연결된 인증 토큰의 만료 시간을 얻기 위해 쿼리가 수행됩니다.

   - 키가 `"DEVICEID"` 그런 다음 현재 장치 id를 얻기 위해 쿼리가 수행됩니다. 이 기능은 기본적으로 비활성화되어 있으며 프로그래머는 Adobe에 지원 및 요금에 대한 정보를 문의해야 합니다.

   - 키가 다음 사용자 메타데이터 유형 목록에 있으면 해당 사용자 메타데이터가 포함된 JSON 개체가 로 전송됩니다 [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) 콜백 함수:

   - `"zip"` - 우편 번호

   - `"encryptedZip"` - 암호화된 우편 번호

   - `"householdID"` - 가구 식별자. MVPD가 하위 계정을 지원하지 않는 경우 이 값은 userID와 동일합니다.

   - `"maxRating"` - 사용자의 최대 유해 컨텐츠 등급

   - `"userID"` - 사용자 식별자입니다. MVPD가 하위 계정을 지원하고 사용자가 기본 계정이 아닌 경우 userID는 familyID와 다릅니다.

   - `"channelID"` - 사용자가 볼 수 있는 채널 목록

   - `"is_hoh"` - 사용자가 가정의 우두머리인지 식별하는 플래그입니다

   - `"encryptedZip"` - 암호화된 우편 번호

   - `"typeID"` - 사용자 계정이 기본/보조 계정인지 식별하는 플래그입니다

   - `"primaryOID"` - 가구 식별자

   - `"postalCode"` - 우편 번호와 유사

   - `"acctID"` - 계정 ID

   - `"acctParentID"` - 계정 상위 ID
   **참고**: 프로그래머가 사용할 수 있는 실제 사용자 메타데이터는 MVPD가 사용할 수 있는 항목에 따라 다릅니다.  자세한 내용은 [사용자 메타데이터](#UserMetadata) 을 참조하십시오.


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
 

**콜백이 트리거됨:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[맨 위로 돌아가기](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**설명:** 사용자가 공급자 선택 UI에서 MVPD를 선택하여 Access Enabler로 공급자 선택을 전송하거나, 사용자가 공급자를 선택하지 않고 공급자 선택 UI를 해제할 경우 null 매개 변수로 이 함수를 호출하면 이 함수를 호출합니다. 

**콜백이 트리거됨:**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[맨 위로 돌아가기](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**설명:** 공급자 선택 대화 상자에서 고객이 선택한 결과를 검색합니다. 초기 인증 확인 후 언제든지 사용할 수 있습니다.

이 함수는 비동기적으로 수행되며 결과를 `selectedProvider()` 콜백 함수입니다.

- **MVPD** 현재 선택한 MVPD이거나 MVPD가 선택되지 않은 경우 null입니다.
- **AE_State** 현재 고객에 대한 인증 결과 &quot;새 사용자&quot;, &quot;사용자가 인증되지 않음&quot; 또는 &quot;사용자 인증됨&quot;

 **콜백이 트리거됨:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[맨 위로 돌아가기](#top)

</br>

## 로그아웃 {#logout}

**설명:** 현재 고객을 로그아웃하고 해당 사용자에 대한 모든 인증 및 인증 정보를 지웁니다. 고객 시스템에서 모든 authN 및 authZ 토큰을 삭제합니다.

 **콜백이 트리거됨:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[맨 위로 돌아가기](#top)

</br>

## 콜백 정의 {#calllback-definitions}

비동기 요청 호출에 대한 응답을 처리하려면 다음 콜백을 구현해야 합니다.

- [entitlloaded()](#entitlementloaded-entitlementloaded)
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

## entitlloaded() {#entitlementLoaded}

**설명:** Access Enabler가 초기화를 완료하고 요청을 받을 준비가 되면 트리거됩니다. 이 콜백을 구현하여 Access Enabler API와의 통신을 시작할 수 있는 시기를 확인합니다.
</br>

[맨 위로 돌아가기](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**설명:** 구성 정보 및 MVPD 목록을 수신하려면 이 콜백을 구현하십시오.

**매개 변수:**

- *configXML*: MVPD 목록을 포함하는 현재 요청자에 대한 구성을 포함하는 xml 개체입니다.

 
**트리거 기준:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[맨 위로 돌아가기](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**설명:** 고유한 사용자 지정 공급자 선택 UI를 호출하려면 이 콜백을 구현합니다. 대화 상자에서 표시 이름(및 선택적 로고)을 사용하여 고객의 선택 사항을 제공해야 합니다. 고객이 선택하고 대화 상자를 해제한 경우 호출에서 선택한 공급자에 대한 관련 ID를 보내십시오 *setSelectedProvider()*.

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

</br>[맨 위로 돌아가기](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**설명:** 사용자가 인증 로그인 페이지 UI를 표시할 iFrame이 필요한 MVPD를 선택한 경우 이 콜백을 구현합니다.

**트리거 기준:**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [맨 위로 돌아가기](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**설명:** 인증 상태를 확인하는 동안 오류가 발생하면 이 콜백을 구현하여 인증 상태(1=authenticated 또는 0=인증되지 않음)와 수사적 오류 메시지를 받습니다(검사가 성공적으로 완료되면 빈 문자열).

>[!NOTE]
> 
>현재를 사용하고 있다면, [고급 오류 보고](/help/authentication/error-reporting.md) 시스템에서 이 함수에 전송된 errorCode 매개 변수를 무시할 수 있습니다.  그러나 isAuthenticated 플래그는 자격 플로우에서 사용자의 인증 상태를 추적하는 데 계속 사용됩니다


**매개 변수:**

- *isAuthenticated* - 인증 상태 제공: 1(인증됨) 또는 0(인증되지 않음)
- *errorCode* - 인증 상태를 확인할 때 발생한 모든 오류 없는 경우 빈 문자열입니다.

 
**트리거 기준:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[맨 위로 돌아가기](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>장치 유형 및 운영 체제는 공용 Java 라이브러리(<http://java.net/projects/user-agent-utils>) 및 사용자 에이전트 문자열입니다. 이 정보는 작업 지표를 장치 카테고리로 분류하는 거친 방법으로만 제공되지만 Adobe이 잘못된 결과에 대해 책임을 지지 않습니다. 따라서 새 기능을 사용하십시오.

**설명:** 특정 이벤트가 발생할 때 추적 데이터를 수신하도록 이 콜백을 구현합니다. 예를 들어 동일한 자격 증명으로 로그인한 사용자 수를 추적하기 위해 이 기능을 사용할 수 있습니다. 추적은 현재 구성할 수 없습니다. Adobe Primetime 인증 1.6을 사용하면, `sendTrackingData()` 디바이스, Access Enabler 클라이언트 및 운영 체제 유형에 대한 정보도 보고합니다. 다음 `sendTrackingData()` 콜백은 이전 버전과 호환됩니다.\
 
- 장치 유형에 사용할 수 있는 값:
   - 컴퓨터
   - 태블릿
   - mobile
   - 게임콘솔
   - 알 수 없음

- Access Enabler 클라이언트 유형에 사용할 수 있는 값:
   - html5
   - ios
   - android


이벤트 유형 및 관련 정보의 배열을 전달합니다. 이벤트 유형은 다음과 같습니다.

| mvpdSelection | 사용자가 공급자 선택 대화 상자에서 MVPD를 선택했습니다. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | 인증 검사가 완료되었습니다. |
| authorizationDetection | 인증 요청이 완료되었습니다. |

</br>
데이터는 각 이벤트 유형에 따라 다릅니다.
</br>

| 이벤트 유형(문자열) | 데이터(어레이) |
|:--- | :--- |
| mvpdSelection | 0: 선택한 MVPD |
|  | 1: 장치 유형 |
|  | 2: Access Enabler 클라이언트 유형 |
|  | 3: OS |
| authenticationDetection | 0: 토큰 요청이 성공했는지 여부(true/false) |
|  | 1: MVPD ID |
|  | 2: GUID |
|  | 3: 토큰이 이미 캐시에 있습니다(true/false). |
|  | 4: 장치 유형 |
|  | 5: Access Enabler 클라이언트 유형 |
|  | 6: OS |
| authorizationDetection | 0: 토큰 요청이 성공했는지 여부(true/false) |
|  | 1: MVPD ID |
|  | 2: GUID |
|  | 3: 토큰이 이미 캐시에 있습니다(true/false). |
|  | 4: 오류 |
|  | 5: 세부 사항 |
|  | 6: 장치 유형 |
|  | 7: Access Enabler 클라이언트 유형 |
|  | 8: OS |


**트리거 기준:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[맨 위로 돌아가기](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**설명:** 이 콜백을 구현하여 인증 요청 또는 확인 권한 부여 요청이 수행되고 성공적으로 완료된 짧은 기간 동안의 미디어 토큰(inToken) 및 리소스의 ID(inRequestedResourceID)를 받습니다.

**트리거 기준:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[맨 위로 돌아가기](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**설명:** 권한 부여 또는 확인 권한 부여 요청이 실패할 때 시그널링할 이 콜백을 구현합니다. 선택적으로 MVPD에서 사용하여 프로그래머가 표시할 사용자 지정 메시지를 제공할 수 있습니다.

>[!IMPORTANT]
>
>이 콜백 함수는 이전 Primetime 인증 오류 보고 시스템의 일부입니다. 이전 버전과의 호환성을 위해 유지되지만, 현재 고급 오류 보고 시스템을 사용하여 자체 콜백을 구현한 경우에는 이 함수를 전혀 사용할 필요가 없습니다. 최신 오류 보고 시스템은 각 오류 또는 경고 유형에 대해 제안된 작업 과정과 함께 인증(또는 기타 작업)이 실패한 이유에 대한 자세한 정보를 제공합니다.

**매개 변수:**

- *inRequestedResourceID* - 인증 요청에 사용된 리소스 ID를 제공하는 문자열입니다.
- *inRequestErrorCode* - 실패 이유를 나타내는 Adobe Primetime 인증 오류 코드를 표시하는 문자열입니다. 가능한 값은 &quot;User Not Authenticated Error&quot; 및 &quot;User Not Authorized Error&quot; 입니다. 자세한 내용은 아래의 &quot;콜백 오류 코드&quot;를 참조하십시오.
- *inRequestDetailedErrorMessage* - 표시에 적합한 추가 설명 문자열입니다. 이 설명 문자열을 어떤 이유로든 사용할 수 없는 경우 Adobe Primetime 인증에서는 빈 문자열을 보냅니다 **(&quot;&quot;)**.  MVPD가 사용자 지정 오류 메시지 또는 판매 관련 메시지를 전달하는 데 사용할 수 있습니다. 예를 들어, 구독자가 리소스에 대한 권한 부여가 거부되면 MVPD가 `*inRequestDetailedErrorMessage*` 예: **&quot;현재 패키지에서 이 채널에 액세스할 수 없습니다. 패키지를 업그레이드하려면 \*여기\*를 클릭합니다.&quot;** 이 콜백을 통해 Programmer의 사이트로 Adobe Primetime 인증을 통해 메시지가 전달됩니다. 그러면 Programmer는 이 옵션을 표시하거나 무시할 수 있습니다. Adobe Primetime 인증에서도 `*inRequestDetailedErrorMessage*` 오류가 발생할 수 있는 조건을 프로그래머에게 알리는 데 사용됩니다. 예, **&quot;공급자의 인증 서비스와 통신하는 동안 네트워크 오류가 발생했습니다.&quot;**

 

**트리거 기준:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[맨 위로 돌아가기](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**설명:** 호출 후 반환된 인증된 리소스 목록을 전달하는 Access Enabler에 의해 트리거되는 콜백 `checkPreauthorizedResources()`.

**매개 변수:**

- *authorizedResources*: 승인된 리소스 목록입니다.

**트리거 기준:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[맨 위로 돌아가기](#top)

</br>

## setMetadataStatus(key, encrypted, data) {#setMetadataStatus(key,encrypted,data)}

**설명:** Access Enabler에 의해 트리거되며, Access Enabler는 `getMetadata()` 호출.

**추가 정보:** [사용자 메타데이터](#userMetadata)

**매개 변수:**

- *키(문자열)*: 요청이 수행된 메타데이터의 키입니다.
- *암호화된(부울)*: &quot;값&quot;이 암호화되어 있는지 여부를 나타내는 플래그입니다. 이 값이 &quot;true&quot;면 &quot;값&quot;은 실제로 실제 값의 JSON 웹 암호화 표현이 됩니다. 
- *데이터(JSON 개체)*: 메타데이터의 표현을 사용하는 JSON 개체입니다.단순 요청(&#39;`TTL_AUTHN``, ``TTL_AUTHZ``, ``DEVICEID`&#39;), 결과는 String(인증 TTL, 인증 TTL 또는 장치 ID를 나타남)입니다. 사용자 메타데이터 요청의 경우 결과는 메타데이터 페이로드를 나타내는 프리미티브 또는 JSON 개체일 수 있습니다. JSON 사용자 메타데이터 개체의 실제 구조는 다음과 유사합니다.

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
[맨 위로 돌아가기](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**설명:** 이 콜백을 구현하여 현재 선택된 MVPD와 `result` 매개 변수. 다음 `result` 매개 변수는 다음 속성을 갖는 객체입니다.

- **MVPD** 현재 선택한 MVPD이거나 MVPD가 선택되지 않은 경우 null입니다.
- **AE\_State** 현재 사용자, &quot;새 사용자&quot;, &quot;인증되지 않은 사용자&quot; 또는 &quot;사용자 인증됨&quot; 중 하나에 대한 인증 결과

 **트리거 기준:** [getSelectedProvider()](#getSelProv)

</br>

[맨 위로 돌아가기](#top)

</br>

### 콜백 오류 코드 {#callback-error-codes}

| 일반 오류 |  |
|:--- | :--- | 
| 내부 오류 | 요청을 처리하는 동안 시스템 오류가 발생했습니다. |
| 공급자가 선택되지 않음 오류 | 고객이 공급자 선택 대화 상자에서 취소할 때 발생합니다 |
| 공급자를 사용할 수 없음 오류 | 공급자를 사용할 수 없을 때 발생합니다. |

| 인증 오류 |  |
|:--- | :--- | 
| 일반 인증 오류 | 이유를 알 수 없거나 게시할 수 없을 때 반환됩니다. |
| 내부 인증 오류 | 인증을 시도하는 동안 시스템 오류가 발생했습니다. |
| 사용자가 인증되지 않은 오류 | 사용자가 인증되지 않았습니다. |
| 여러 인증 요청 오류 | 첫 번째 인증 요청이 완료되기 전에 추가 인증 요청을 받았습니다. |

| 인증 오류 |  |
|:--- | :--- | 
| 일반 인증 오류 | 이유를 알 수 없거나 게시할 수 없을 때 반환됩니다. |
| 내부 권한 부여 오류 | 권한을 부여하려는 동안 시스템 오류가 발생했습니다. |
| 사용자가 승인되지 않은 오류 | 고객은 요청된 컨텐츠를 볼 수 있는 권한이 없습니다. |

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

