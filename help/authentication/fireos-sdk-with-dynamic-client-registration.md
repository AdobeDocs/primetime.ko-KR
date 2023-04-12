---
title: Amazon FireOS SDK 및 Dynamic Client Registration
description: Amazon FireOS SDK 및 Dynamic Client Registration
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---


# Amazon FireOS SDK 및 Dynamic Client Registration {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>

## <span id=""></span>소개 {#Intro}

FireTV용 FireOS AccessEnabler SDK가 세션 쿠키를 사용하지 않고 인증을 사용하도록 수정되었습니다. 점점 더 많은 브라우저가 쿠키에 대한 액세스를 제한하므로 인증을 허용하려면 다른 방법이 필요합니다.

**FireOS SDK 3.0.4** 는 서명된 요청자 ID 및 세션 쿠키 인증을 기반으로 현재 앱 등록 메커니즘을 [동적 클라이언트 등록](/help/authentication/dynamic-client-registration.md).
 

## API 변경 사항 {#API}

### Factory.getInstance

**설명:** Access Enabler 개체를 인스턴스화합니다. 애플리케이션 인스턴스마다 단일 Access Enabler 인스턴스가 있어야 합니다.

| API 호출: 생성자 |
| --- |
| public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        AccessEnablerException 실행 |

**사용 가능:** v3.0+

**매개 변수:**

- *appContext*: Android 애플리케이션 컨텍스트
- *softwareStatement*: TVE 대시보드에서 가져온 값 또는 *null* string.xml에 &quot;software\_statement&quot;가 설정된 경우
- *redirectUrl* : fireTV 구현의 경우 이 매개 변수는 null이어야 합니다. 이 특성의 모든 설정은 무시됩니다. 

**참고**

- 잘못된 softwareStatement로 인해 응용 프로그램이 AccessEnabler를 초기화하거나 Adobe Pass 인증 및 권한 부여에 응용 프로그램을 등록하지 않습니다.
- FireTV용 redirectUrl 매개 변수는 SDK에서 adobepass://android.app as 인증으로 설정되어 고유한 AccessEnabler 인스턴스에 의해 처리됩니다.

### setRequestor

**설명:** 채널의 ID를 설정합니다. Adobe Primetime 인증 시스템의 Adobe에 등록하면 각 채널에 고유 ID가 할당됩니다. SSO 및 원격 토큰을 처리할 때 응용 프로그램이 백그라운드에 있을 때 인증 상태를 변경할 수 있습니다. 시스템 상태와 동기화하기 위해 응용 프로그램을 포그라운드로 가져올 때 setRequestor를 다시 호출할 수 있습니다(SSO가 활성화된 경우 원격 토큰을 가져오거나 그 동안 로그아웃이 발생한 경우 로컬 토큰을 삭제).

서버 응답에는 MVPD 목록과 채널의 ID에 첨부된 일부 구성 정보가 포함되어 있습니다. 서버 응답은 Access Enabler 코드에서 내부적으로 사용됩니다. 작업 상태(즉, SUCCESS/FAIL)만 setRequestorComplete() 콜백을 통해 애플리케이션에 표시됩니다.

만약 *url* 매개 변수가 사용되지 않으면 결과 네트워크 호출은 기본 서비스 공급자 URL을 타겟으로 합니다. Adobe 릴리스 프로덕션 환경입니다.

에 값이 제공된 경우 *url* 매개 변수, 결과 네트워크 호출은 *url* 매개 변수. 모든 구성 요청은 별도의 스레드에서 동시에 트리거됩니다. MVPD 목록을 컴파일할 때 첫 번째 응답기가 우선합니다. 목록에 있는 각 MVPD에 대해 Access Enabler는 연관된 서비스 공급자의 URL을 기억합니다. 이후의 모든 자격 요청은 구성 단계 동안 대상 MVPD와 연결된 서비스 공급자와 연결된 URL로 전달됩니다.

| API 호출: 요청자 구성 |
| --- |
| public void setRequestor(String requestorId) |

**사용 가능:** v3.0+

| API 호출: 요청자 구성 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**사용 가능:** v3.0+

**매개 변수:**

- *requestorID*: 채널과 연관된 고유 ID입니다. Adobe Primetime 인증 서비스에 처음 등록할 때 Adobe에서 할당한 고유 ID를 사이트에 전달합니다.
- *url*: 선택적 매개 변수; 기본적으로 Adobe 서비스 공급자가 사용됩니다(http://sp.auth.adobe.com/). 이 배열을 사용하면 Adobe에서 제공하는 인증 및 인증 서비스의 끝점을 지정할 수 있습니다(다른 인스턴스는 디버깅 목적으로 사용될 수 있음). 이를 사용하여 여러 Adobe Primetime 인증 서비스 공급자 인스턴스를 지정할 수 있습니다. 이때 MVPD 목록은 모든 서비스 공급자의 끝점으로 구성됩니다. 각 MVPD는 가장 빠른 서비스 공급자와 연결됩니다. 즉, 먼저 응답하고 해당 MVPD를 지원하는 공급자입니다.

사용되지 않음:

- *signedRequestorID*: 개인 키로 디지털 서명된 요청자 ID의 사본. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**콜백이 트리거됨:** `setRequestorComplete()`

</br>

### 로그아웃

**설명:** 이 메서드를 사용하여 로그아웃 흐름을 시작합니다. 로그아웃은 사용자가 Adobe Primetime 인증 서버 및 MVPD 서버에서 모두 로그아웃해야 하기 때문에 일련의 HTTP 리디렉션 작업이 발생한 결과입니다. 따라서 이 흐름은 ChromeCustomTab 창을 열어 로그아웃합니다.

| API 호출: 로그아웃 흐름 시작 |
| --- |
| public void logout() |

**사용 가능:** v3.0+

**매개 변수:** 없음

**콜백이 트리거됨:** `setAuthenticationStatus()`

## 프로그래머 구현 흐름 {#Progr}

### **1. 애플리케이션 등록** 

1. Adobe Pass에서 software\_statement 가져오기( TVE Dashboard )
1. 이러한 값을 Adobe Pass SDK에 전달하는 두 가지 옵션이 있습니다.
   - strings.xml에서 를 추가합니다. 

      ```
      <string name>"software\_statement">[softwarestatement value]</string>
      ```

   - AccessEnabler.getInstance(appContext,softwareStatement, null)를 호출합니다.

 

### **2. 애플리케이션 구성**

- a.  setRequestor(requestor\_id) 

   SDK는 다음 작업을 수행합니다. 

   - 등록 신청: 사용 **software\_statement**&#x200B;를 입력하면 SDK는 **client\_id, client\_secret, client\_id\_issued\_at, redirect\_url, grant\_types**. 이 정보는 애플리케이션의 내부 스토리지에 저장됩니다.
   - 얻다 **access\_token** client\_id, client\_secret 및 grant\_type=&quot;client\_credentials&quot; 사용. 이 액세스\_token은 SDK가 Adobe Pass 서버에 대해 수행하는 각 호출에서 사용됩니다.

| 토큰 오류 응답 : |  |  |
|--- | --- | --- |
| HTTP 400(잘못된 요청) | {&quot;error&quot;: &quot;invalid\_request&quot;} | 요청에 필요한 매개 변수가 없거나, 지원되지 않는 매개 변수 값(그랜트 유형 제외)이 포함되어 있거나, 매개 변수를 반복하거나, 여러 자격 증명을 포함하거나, 클라이언트를 인증하기 위해 두 개 이상의 메커니즘을 사용하거나, 그렇지 않은 경우 형식이 잘못되었습니다. |
| HTTP 400(잘못된 요청) | {&quot;error&quot;: &quot;invalid\_client&quot;} | 클라이언트를 알 수 없어서 클라이언트 인증에 실패했습니다. SDK *필수* 인증 서버에 다시 등록하십시오. |
| HTTP 400(잘못된 요청) | {&quot;error&quot;: &quot;unauthorized\_client&quot;} | 인증된 클라이언트가 이 권한 부여 형식을 사용할 수 있는 권한이 없습니다. |

- MVPD에 수동 인증이 필요한 경우 WebView가 열려 해당 MVPD를 사용하여 수동적이며 완료되면 닫힙니다

- b. checkAuthentication()

   - *true* : 권한 부여로 이동
   - *false* : MVPD 선택으로 이동

- c. getAuthentication : SDK에는 다음이 포함됩니다 **access_token** 호출 매개 변수 

   - mvpd가 기억함 : setSelectedProvider(mvpd\_id)로 이동합니다.
   - mvpd를 선택하지 않았습니다. displayProviderDialog
   - mvpd가 선택함 : setSelectedProvider(mvpd\_id)로 이동합니다.

- d. setSelectedProvider

   - mvpd\_id 인증 url이 ChromeCustomTabs에 로드됩니다.
   - 로그인 성공 : delegate.setAuthenticationStatus( SUCCESS )
   - 로그인 취소됨 : MVPD 선택 재설정
   - URL 체계는 인증이 완료되면 캡처하도록 &quot;adobepass://android.app&quot;으로 설정됩니다

- e. get/checkAuthorization : SDK는 권한 부여로 헤더에 **access\_token **을 포함합니다. 베어러 **access\_token**

- 인증이 성공하면 미디어 토큰을 얻기 위한 호출이 수행됩니다

- f. 로그아웃 : 

   - SDK는 현재 요청자에 대한 유효한 토큰을 삭제합니다(SSO를 통해 획득되지 않고 다른 애플리케이션에서 획득한 인증은 유효함)
   - SDK가 Chrome 사용자 지정 탭을 열어 mvpd\_id 로그아웃 종단점에 도달합니다. 완료되면 Chrome 사용자 지정 탭이 닫힙니다
   - URL 체계는 &quot;adobepass://logout&quot;으로 설정되어 로그아웃이 완료되면 해당 순간을 캡처합니다
   - 로그아웃은 sendTrackingData(새 이벤트(EVENT\_LOGOUT, USER\_NOT\_AUTHENTICATED\_ERROR) 및 콜백을 트리거합니다. setAuthenticationStatus(0,&quot;Logout&quot;)

 

**참고:** 각 호출에는 **access_token**, 아래의 가능한 오류 코드는 SDK에서 처리됩니다. 

| 오류 응답 |  |  |
|--- | --- | --- |
| invalid_request | 400 | 요청의 형식이 잘못되었습니다. SDK는 서버 호출 수행을 중지해야 합니다. |
| invalid_client | 403 | 클라이언트 ID는 더 이상 요청을 수행할 수 없습니다. SDK는 클라이언트 등록을 다시 수행해야 합니다. |
| access_denied | 401 | access_token이 잘못되었습니다. sdk는 새 access_token을 요청해야 합니다. |

