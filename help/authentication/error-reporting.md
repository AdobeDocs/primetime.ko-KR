---
title: 오류 보고
description: 오류 보고
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# 오류 보고 {#error-reporting}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.


## 개요 {#overview}

Adobe Primetime 인증의 오류 보고는 현재 두 가지 방법으로 구현되었습니다.

* **고급 오류 보고** 구현자는 [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) 또는 &quot;`status`&quot; [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) 및 [AccessEnabler Android SDK](#accessenabler-android-sdk)고급 오류 보고를 수신하려면 를 선택합니다. 오류는 다음과 같이 분류됩니다 **정보**, **경고**, 및 **오류** 유형. 이 보고 시스템은 **비동기**, 및에 전송됩니다. **여러 오류가 트리거되는 순서에 대한 보장이 없습니다**.  고급 오류 보고 시스템에 대한 자세한 내용은 [고급 오류 보고](#advanced-error-reporting) 섹션을 참조하십시오.

* **원래 오류 보고 -** 특정 요청이 실패할 때 오류 메시지가 특정 콜백 함수에 전달되는 정적 보고 시스템입니다. 오류는 일반, 인증 및 인증 유형으로 그룹화됩니다. 원래 시스템에 보고된 오류 목록을 보려면 [원래 오류 보고](#original-error-reporting) 섹션을 참조하십시오.


## 고급 오류 보고 {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>오래된 [원래 오류 보고](#original-error-reporting) API는 이전과 동일하게 계속 작동하며 고급 오류 보고에서는 기능을 중단하지 않지만, 원래 오류 보고에서는 더 이상 업데이트를 받지 않습니다. 모든 새로운 오류 및 업데이트가 고급 오류 보고 시스템에 발생합니다.

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

새 오류 보고 시스템은 선택 사항이므로 구현자가 고급 오류 보고서를 받기 위해 오류 처리기 콜백을 명시적으로 등록할 수 있습니다. 시스템에 여러 오류 콜백을 동적으로 등록 및 등록 취소하는 기능이 포함되어 있습니다. 또한 AccessEnabler JavaScript SDK가 로드되는 즉시(를 호출하기 전에) 다른 초기화를 수행하지 않고도 새로운 오류 콜백을 등록할 수 있습니다 `setRequestor()`). 즉, 초기화 및 구성 오류에 대한 고급 보고서를 받을 수 있습니다.


#### 구현 {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


오류 처리기 콜백 함수는 다음 구조의 단일 개체(맵)를 수신합니다.

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1. 바인딩 {#bind}

**`.bind(eventType:String, handlerName:String):void`**

이벤트의 처리기를 연결합니다.

**`eventType`** - &quot;`errorEvent`&quot; 값을 지정하면 AccessEnabler JavaScript SDK에서 고급 오류 보고서 콜백을 트리거합니다.

**`handlerName`** - 오류 처리기 함수의 이름을 지정하는 문자열입니다.\
 

두 바인딩 매개 변수는 모두 다음 집합의 문자만 사용해야 합니다. `[0-9a-zA-Z][-._a-zA-Z0-9]`; 즉, 매개 변수는 숫자나 문자로 시작해야 하며 하이픈, 마침표, 밑줄 및 영숫자만 포함할 수 있습니다.  또한 매개 변수는 1024자를 초과할 수 없습니다.  

**예** 바인딩 오류 처리기:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

기술 제한 사항으로 인해 닫기 또는 익명 함수를 바인딩할 수 없습니다. 두 번째 매개 변수에서 메서드 이름을 지정해야 합니다.

 
### 2. 바인딩 해제 {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

이전에 연결된 이벤트 처리기를 제거합니다.

**`eventType`** - &#39;`errorEvent`&#39; 값은 AccessEnabler JavaScript SDK에서 고급 오류 보고서 콜백을 트리거합니다.

**`handlerName`** - 오류 처리기 함수의 이름을 지정하는 문자열(가 null이거나 지정된 처리기에 첨부된 모든 처리기가 없는 경우) `eventType` 이 제거됩니다.

두 바인딩 매개 변수는 모두 다음 집합의 문자만 사용해야 합니다. `[0-9a-zA-Z][-._a-zA-Z0-9]`; 즉, 매개 변수는 숫자나 문자로 시작해야 하며 하이픈, 마침표, 밑줄 및 영숫자만 포함할 수 있습니다.  또한 매개 변수는 1024자를 초과할 수 없습니다.  

**예** 단일 오류 처리기를 제거하는 방법:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**예** 모든 오류 처리기를 제거합니다.

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

새 오류 보고 시스템은 필수입니다. 따라서 구현자는 새 Objective C &quot;EntitlementStatus&quot; 프로토콜을 명시적으로 준수해야 합니다. 이 새로운 접근 방식을 통해 프로그래머는 고급 오류 보고를 받을 수 있습니다.

#### 구현 {#accessenab-ios-tvossdk-imp}

구현자는 다음 사항을 준수해야 합니다 **권한 상태** 프로토콜:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

사용자 **상태** 함수는 단일 개체( `NSDictionary`) 내의 구조를 확인합니다.

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. 선언**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. 구현**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

새 오류 보고 시스템은 구현자가 명시적으로 `IAccessEnablerDelegate` 인터페이스 정의 프로토콜입니다. 이 새로운 접근 방식을 통해 프로그래머는 고급 오류 보고를 받을 수 있습니다.

#### 구현 {#access-enablr-androidsdk-imp}

구현자가 새 `status` 인터페이스의 메서드`IAccessEnablerDelegate`. 다음 **`status`** 함수는 **`AdvancedStatus`** 다음 모델이 있는 객체:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**샘플**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


새 오류 보고 시스템은 구현자가 명시적으로 `IAccessEnablerDelegate` 인터페이스 정의 프로토콜입니다. 이 새로운 접근 방식을 통해 프로그래머는 고급 오류 보고를 받을 수 있습니다.

#### 구현 {#access-enab-fireos-sdk-}

구현자가 새 `status`인터페이스의 메서드`IAccessEnablerDelegate`. 다음 **`status`** 함수는 **`AdvancedStatus`** 다음 모델이 있는 객체:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**샘플**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## 고급 오류 코드 참조 {#advanced-error-codes-reference}

다음 표는 새로운 오류 API에 의해 노출된 오류 코드와 이를 해결하기 위해 취할 제안된 작업을 나열하고 설명합니다.

| ID | 수준 | 설명 | 개발자 작업 | 사용자 작업 | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL 및 AAPL_ERROR | 오류 | 일반 Apple SSO 오류 | 오류에 원래 VSA 오류가 있는 세부 정보 필드가 포함되어 있습니다. | n/a | n/a | 예 | n/a |
| VSA203 | 정보 | 플랫폼 SSO를 통한 로그인의 결과로 인증이 발생한 동안 사용자가 응용 프로그램에서 로그아웃하기로 결정했습니다. | tvOS에서 설정 -> 계정 -> TV 공급자에서 명시적으로 로그아웃하도록 사용자에게 지시하거나 메시지를 표시합니다. <br><br> iOS/iPadOS의 설정 -> TV 공급자에서 명시적으로 로그아웃하도록 사용자에게 지시하거나 메시지를 표시합니다. | tvOS의 설정 -> 계정 -> TV 공급자에서 명시적으로 로그아웃합니다. <br> <br> iOS/iPadOS의 설정 -> TV 공급자에서 명시적으로 로그아웃합니다 | n/a | 예 | n/a |
| VSA404 | 정보 | 응용 프로그램 비디오 구독자 계정 권한이 확인되지 않았습니다. | SSO(Single Sign-On) 사용자 경험의 이점을 설명함으로써 구독 정보에 액세스할 수 있는 권한을 부여하지 않는 사용자에게 인센티브를 제공합니다. | 사용자는 애플리케이션 설정(TV 공급자 액세스)으로 이동하거나, 설정 -> iOS/iPadOS의 TV 공급자 설정 또는 설정 -> 계정 -> tv Provider에서 섹션으로 이동하여 결정을 변경할 수 있습니다. | n/a | 예 | n/a |
| VSA503 | 정보 | 응용 프로그램 비디오 구독자 계정 메타데이터 요청이 실패했습니다. | MVPD 끝점이 응답하지 않습니다. 애플리케이션이 일반 인증 흐름에 폴백할 수 있습니다. | n/a | n/a | 예 | n/a |
| 500 | 오류 | 내부 오류 | AccessEnablerDebug를 사용하여 디버그 로그(console.log 출력)를 검사하여 문제가 발생했는지 확인합니다. | n/a | 예 | 예 | n/a |
| SEC403 | 오류 | 도메인 보안 오류입니다. 요청자가 잘못된 도메인을 사용하고 있습니다. 특정 요청자 ID에서 사용하는 모든 도메인은 Adobe에서 화이트리스트에 추가해야 합니다. | - 허용된 도메인 목록에서만 AccessEnabler를 로드합니다 <br> <br> - 사용된 요청자 ID에 대한 도메인 허용 목록을 관리하려면 Adobe에 문의하십시오 <br> <br> - iOS: 올바른 인증서를 사용하고 있으며 서명이 제대로 작성되었는지 확인합니다 | n/a | n/a | 예 | n/a |
| SEC412 | 경고 | [ 릴리스 2.5에서 사용 가능 ] 장치 ID가 일치하지 않습니다. 이 문제는 기본 플랫폼이 장치 ID를 변경할 때마다 발생할 수 있습니다. 이 경우 기존 토큰이 지워지고 사용자가 더 이상 인증되지 않습니다. 사용자가 JS SDK를 사용하고 로밍(JS에서 클라이언트 IP는 장치 ID의 일부)을 사용하는 경우 합법적으로 이러한 문제가 발생합니다. 그렇지 않으면 사기 시도를 나타내는 것일 수 있습니다. 다른 장치에서 토큰을 복사하려는 시도입니다. | - 경고 수를 모니터링합니다. 명백한 이유 없이 급증하는 경우(최근 브라우저 업데이트 없음) 사기 시도의 지표가 될 수 있는 새로운 운영 체제).  <br> <br>- 원할 경우 다시 로그인해야 한다고 사용자에게 알립니다. | 다시 로그인합니다. | 예 | 예 | 예(3.2부터) |
| SEC420 | 오류 | Adobe Primetime 인증 서버와 통신하는 동안 HTTP 보안 오류가 발생했습니다. 이 오류는 일반적으로 스푸핑/프록시가 있는 경우 발생합니다. | - 로드 `[https://]{SP_FQDN\}` 브라우저에서 수동으로 SSL 인증서를 허용합니다(예: **https://api.auth.adobe.com** 또는 **https://api.auth-staging.adobe.com** <br> <br>- 프록시 인증서를 신뢰할 수 있는 것으로 표시 | 일반 사용자에게 이러한 문제가 발생할 경우, 이것은 가능한 중간 공격에 대한 표시입니다! | 예 | 예 | 예(3.2부터) |
| CFG100 | 경고 | 클라이언트 컴퓨터 날짜/시간/시간대가 올바르게 설정되지 않았습니다. 이로 인해 인증/인증 오류가 발생할 수 있습니다. | - 사용자에게 올바른 시간을 설정하도록 알립니다. <br> <br> 자격 흐름이 실패할 수 있으므로 권한 흐름을 방지하기 위한 조치를 취합니다. | 올바른 날짜/시간을 설정합니다. | 예 | 예 | 예(3.2부터) |
| CFG400 | 오류 | 잘못된 요청자 ID를 제공했습니다. | 개발자가 유효한 요청자 ID를 지정해야 합니다. | n/a | 예 | 예 | 예(3.2부터) |
| CFG404 | 오류 | Adobe Primetime 인증 서버를 찾을 수 없습니다. 이 문제는 다음 3개 인스턴스에서 발생할 수 있습니다. <br><br> - 개발자가 잘못된 스푸핑을 배치합니다. <br><br> -사용자에게 네트워킹 문제가 있으며 Adobe Primetime 인증 도메인에 연결할 수 없습니다. <br><br> -Adobe Primetime 인증 서버가 잘못 구성되었습니다. <br><br>  **참고:** Firefox에서 CFG400 이 CFG404 대신 나타납니다(브라우저 제한 사항) | - 스푸핑을 확인합니다. <br><br> -네트워크/DNS 설정을 확인합니다. <br><br> -Adobe 알림. | 네트워크/DNS 설정을 확인합니다. | 예 | 예 | 예(3.2부터) |
| CFG410 | 오류 | AccessEnabler가 너무 오래되었습니다. | 사용자에게 캐시를 지우도록 알립니다. | 브라우저 캐시를 지웁니다. | 예 | n/a | 예(3.2부터) |
| CFG5xx | 오류 | Adobe Primetime 인증 서버에 내부 오류가 발생했습니다. xx 는 임의의 번호일 수 있습니다. | - Adobe Primetime 인증을 사용할 수 없음을 사용자에게 알립니다. <br><br> - Adobe Primetime 인증 무시. <br> <br> - Adobe 알림. | 나중에 시도하십시오. | 예 | 예 | 예(3.2부터) |
| N000 | 정보 | 사용자가 인증되지 않았습니다. | n/a | 로그인. | 예 | 예 | 예(3.2부터) |
| N001 | 정보 | 백그라운드에서 수동 인증 시도가 시작되었습니다. 이 작업은 &quot;요청자별 인증&quot;으로 구성된 MVPD에 대해 발생합니다. 사용자가 자동으로 인증될 수 있지만 이는 초기화 시 성능 처벌을 받게 됩니다. | 선택적으로 사용자에게 알리거나 사용자에게 &quot;작업이 진행 중&quot;이라고 알려주는 UI를 제공할 수 있습니다. | 잠깐 | 예 | 예 | 예(3.2부터) |
| N003 | 정보 | 사용자가 Apple MVPD 선택기에서 &quot;기타 TV 공급자&quot; 옵션을 선택합니다. | 다음 *displayProviderDialog* 콜백이 호출되고, 응용 프로그램이 일반 인증 흐름으로 폴백될 수 있습니다. | 일반 MVPD를 선택하고 로그인 화면을 계속 진행합니다. | n/a | 예 | n/a |
| N004 | 정보 | 사용자가 현재 요청자가 지원하지 않는 TV 공급자를 선택합니다. | 다음 *displayProviderDialog* 콜백이 호출되고, 응용 프로그램이 일반 인증 흐름으로 폴백될 수 있습니다. | 일반 MVPD를 선택하고 로그인 화면을 계속 진행합니다. | n/a | 예 | n/a |
| N005 | 정보 | MVPD 선택기가 취소되었습니다. | n/a | n/a | 예 | 예 | 예(3.2부터) |
| N010 | 경고 | 선택한 MVPD에 대해 인증-모두 저하 규칙이 적용되는 동안 사용자가 인증되었습니다. | 선택적으로 사용자에게 MVPD의 문제로 인해 &quot;무료&quot; 액세스를 받고 있음을 알립니다. | n/a | 예 | 예 | 예(3.2부터) |
| N011 | 정보 | 사용자가 TempPass를 사용하여 인증되었습니다. | - 사용자에게 알립니다. <br> <br> - 원할 경우 일반 MVPD 목록을 제공합니다. | 원할 경우 일반 MVPD로 로그인합니다. | 예 | 예 | 예(3.2부터) |
| N111 | 경고 | 만료된 TempPass. | - 사용자에게 알립니다. <br> <br> - 일반 MVPD 목록 표시 <br> <br> - TempPass 옵션을 숨깁니다. | 일반 MVPD로 로그인합니다. | 예 | 예 | 예(3.2부터) |
| N130 | 오류 | **세션에서 인증 토큰을 찾을 수 없습니다.**  다음 중 하나가 원인일 수 있습니다. <br> <br> 1. 브라우저에 (타사) 쿠키가 비활성화되어 있음(AccessEnabler JavaScript SDK 버전 4.x에는 해당되지 않음) <br> <br> 2. 브라우저에 사이트 간 추적 방지 기능이 활성화됨(Safari 11 이상) <br> <br> 3. 세션이 만료되었습니다. <br> <br> 4. 프로그래머가 잘못된 연속으로 인증 API를 호출합니다 <br> <br> 참고: 이 오류 코드는 전체 페이지 리디렉션 인증 흐름에 사용할 수 없습니다. | 1. 사용자에게 (타사) 쿠키를 활성화하라는 메시지 표시 <br> <br> 2. 사이트 간 추적을 비활성화하도록 프로필 사용자 <br> <br> 3. 사용자에게 재인증 확인 <br> <br> 4. 올바른 순서로 API 호출 | 1. (타사) 쿠키를 활성화합니다 <br> <br> 2. 사이트 간 추적 비활성화 <br> <br> 3. 재인증 <br> <br> 4. 해당 없음 | 예 | 예 | 예(3.2부터) |
| N500 | 오류 | 내부 오류입니다. <br> <br> 참고: 이것은 원래 오류 시스템의 &quot;일반 인증 오류&quot; 및 &quot;내부 인증 오류&quot;입니다. 이 오류는 결국 단계적으로 중단됩니다. | AccessEnablerDebug를 사용하여 디버그 로그(console.log 출력)를 검사하여 문제가 발생했는지 확인합니다. | n/a | 예 | 예 | n/a |
| R401 | 오류 | 액세스 토큰을 가져오는 동안 오류가 발생했습니다. <br> <br> 참고: 복구할 수 없는 오류입니다. 응용 프로그램을 사용할 수 없음을 사용자에게 알립니다. | - iOS: 응용 프로그램에서 소프트웨어 문과 사용자 지정 체계를 확인합니다. <br> <br> - JavaScript: 웹 사이트 애플리케이션에서 소프트웨어 구문을 확인합니다. <br> <br> Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다 | n/a | 예 v4.0에서 | 예 v3.0에서 | 예(3.2부터) |
| R400 | 오류 | 응용 프로그램이 등록되지 않았습니다. 소프트웨어 문이 잘못되었거나 해지되었습니다. <br> <br> 참고: 복구할 수 없는 오류입니다. 응용 프로그램을 사용할 수 없음을 사용자에게 알립니다. | - iOS: 응용 프로그램에서 소프트웨어 문과 사용자 지정 체계를 확인합니다. <br> <br> - JavaScript: 웹 사이트 애플리케이션에서 소프트웨어 구문을 확인합니다. <br> <br> Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다 | n/a | 예 v4.0에서 | 예 v3.0에서 | 예(3.2부터) |
| REG500 | 오류 | 서버에서 등록 코드를 가져올 수 없습니다. <br> <br> 참고: 복구할 수 없는 오류입니다. 응용 프로그램을 사용할 수 없음을 사용자에게 알립니다. | Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다. | n/a | 예 v4.0에서 | 예 v3.0에서 | 예(3.2부터) |
| REGCODE | 성공 | tvOS 플랫폼에서 setSelectedProvider API라고 하는 응용 프로그램입니다. | 사용자에게 제공된 등록 코드를 사용하여 로그인하도록 두 번째 장치(화면)를 사용하도록 지시/묻습니다. | 두 번째 장치(화면)에서 regcode를 사용하여 인증을 시작합니다. | n/a | 예 tvOS에서만 | n/a |
| Z010 | 경고 | 선택한 MVPD에 대해 인증-모두 또는 권한 부여-모든 성능 저하 규칙이 적용되는 동안 사용자가 인증되었습니다. | 선택적으로 사용자에게 MVPD의 문제로 인해 &quot;무료&quot; 액세스를 받고 있음을 알립니다. | n/a | 예 | 예 | 예(3.2부터) |
| Z011 | 정보 | 사용자가 TempPass를 사용하여 인증되었습니다. | 선택적으로 사용자에게 알림 | n/a | 예 | 예 | 예(3.2부터) |
| Z100 | 오류 | 요청한 리소스에 대한 구독이 없거나 MVPD에서 시작된 다른 이유로 인해 권한 부여가 실패했습니다. 예를 들어 비디오가 사용자 계정에 대한 자녀 보호 설정과 일치하지 않습니다 | - 재생을 허용하지 않습니다. <br> <br> - 사용자에게 알립니다. <br> <br> - 오류 메시지의 &#39;message&#39; 키에 MVPD가 제공하는 보다 자세한 메시지가 포함될 수 있습니다. | n/a | 예 | 예 | 예(3.2부터) |
| Z110 | 오류 | MVPD의 부인으로 인해 권한이 거부되었습니다. 사기 시도 또는 DOS가 있습니다. | - 재생을 허용하지 않습니다. <br> <br> - 사용자에게 알립니다. | n/a | 예 | 예 | 예(3.2부터) |
| Z120 | 오류 | MVPD와 통신하는 데 기술적인 이유로 인증이 거부되었습니다. 가능한 네트워크 오류입니다. | - 재생을 허용하지 않습니다. <br> <br> - 사용자에게 MVPD가 어려움을 겪고 나중에 시도해야 한다고 알립니다. | 나중에 시도하십시오. | 예 | 예 | 예(3.2부터) |
| Z130 | 오류 | 잘못된 / 잘못된 형식의 리소스를 사용하므로 권한 부여가 거부되었습니다. | 리소스 문자열을 확인하고 수정합니다. 일반적으로 이 오류는 잘못된 포맷의 MRSS이거나 MRSS 대신 일반 문자열을 사용하기 때문입니다. | n/a | 예 | 예 | 예(3.2부터) |
| Z169 | 오류 | 지정된 리소스에 대해 authNone 저하 규칙이 적용되었기 때문에 인증이 거부되었습니다. | 사용자에게 알림 | n/a | 예 | 예 | 예(3.2부터) |
| Z500 | 오류 | 내부 오류입니다. <br> <br>  참고: 기존 &quot;일반 인증 오류&quot; 및 &quot;내부 인증 오류&quot;입니다. 이 오류는 결국 단계적으로 중단됩니다. | AccessEnablerDebug를 사용하여 디버그 로그(console.log 출력)를 검사하여 문제가 발생했는지 확인합니다. | n/a | 예 | 예 | 예(3.2부터) |
| P100 | 오류 | 사전 권한 부여에 실패했습니다. 이는 너무 많은 리소스에 대한 권한 부여 요청 때문일 수 있습니다. | - 허용된 최대 리소스 수를 초과하여 사용하지 마십시오. <br> <br> - 허용되는 최대 리소스 수를 찾아서 설정하려면 Adobe Primetime 인증 지원 센터에 문의하십시오. | n/a | 예 v3.0에서 | 예 | 예(3.2부터) |
| IS2XX | 오류 | 이러한 오류 코드는 개인화 서버 끝점 응답 데이터의 형식이 잘못되었거나 필요한 개인화 정보가 누락되었을 때 반환됩니다. | Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다 | n/a | 예 v3.0에서 | n/a | n/a |
| IS4XX | 오류 | 이러한 오류 코드는 개인화 서버 엔드포인트 실패 4XX 인 경우 응답의 HTTP 상태 코드로 반환됩니다. | Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다 | n/a | 예 v3.0에서 | n/a | n/a |
| IS5XX | 오류 | 이러한 오류 코드는 개별화 서버 끝점 실패 5XX 인 경우 반환되며, 이 응답의 HTTP 상태 코드입니다. | Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다 | n/a | 예 v3.0에서 | n/a | n/a |
| IS0 | 오류 | 이 코드는 개인화 서버 끝점이 전혀 응답하지 않아 연결 시간이 초과되면 반환됩니다 | Zendesk를 사용하여 티켓을 열고 시스템을 일시적으로 사용할 수 없음을 사용자에게 알립니다 | n/a | 예 v3.0에서 | n/a | n/a |
| LS011 | 경고 | AccessEnabler는 LSO/LocalStorage 문제와 WebStorage 문제(또는 비가용성)로 인해 휘발성 스토리지를 사용하고 있습니다. <br> <br> 인증/권한 부여가 현재 페이지 이상으로 지속되지 않습니다. 각 페이지를 로드하면 사용자가 인증해야 합니다. 구성된 TTL은 페이지 다시 로드 간에 적용되지 않습니다. | - 사용자에게 제한 사항을 알립니다. <br> <br> - 사용 가능한 저장 공간을 늘리는 방법을 사용자에게 알려줍니다. <br> <br> - 또는 로그아웃하여 저장소를 지웁니다. | - 스토리지 증가 <br> <br> - 저장소를 지우려면 로그아웃합니다. | 예 | n/a | n/a |

<br>

## 원래 오류 보고 {#original-error-reporting}

이 섹션에서는 원래 오류 코드와 함께 원래 오류 보고 시스템에 대해 설명합니다. 원래 오류 보고 시스템에서 AccessEnabler는 다음 두 콜백 함수에 오류를 전달합니다. `setAuthenticationStatus()` 호출 후 `checkAuthentication()`; `tokenRequestFailed()`호출 실패 후 `checkAuthorization()` 또는 `getAuthorization()`.

원래 오류 보고 및 상태 API는 이전과 동일하게 계속 작동합니다. 하지만 앞으로는 원래 오류 보고 API가 업데이트되지 않습니다. 이전 오류에 대한 새로운 오류 보고 및 업데이트는 2010년에만 반영됩니다 [고급 오류 보고 시스템](#advanced-error-reporting).


원래 오류 보고 시스템을 사용하는 예는 를 참조하십시오. [JavaScript API 참조](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) 및 [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) 함수, [iOS/tvOS API 참조](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)및 [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Android API 참조](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) 및 [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### 원래 콜백 오류 코드 {#original-callback-error-codes}

| **일반 오류** |  |
|---|---|
| 내부 오류 | 요청을 처리하는 동안 시스템 오류가 발생했습니다. |
| 공급자가 선택되지 않음 오류 | 고객이 공급자 선택 대화 상자에서 취소할 때 발생합니다. |
| 공급자를 사용할 수 없음 오류 | 공급자를 사용할 수 없을 때 발생합니다. |
|  |  |
| **인증 오류** |  |
| 일반 인증 오류 | 이유를 알 수 없거나 게시할 수 없을 때 반환됩니다. |
| 내부 인증 오류 | 인증을 시도하는 동안 시스템 오류가 발생했습니다. |
| 사용자가 인증되지 않은 오류 | 사용자가 인증되지 않았습니다. |
|  |  |
| **인증 오류** |  |
| 일반 인증 오류 | 이유를 알 수 없거나 게시할 수 없을 때 반환됩니다. |
| 내부 권한 부여 오류 | 권한을 부여하려는 동안 시스템 오류가 발생했습니다. |
| 사용자가 승인되지 않은 오류 | 고객은 요청된 컨텐츠를 볼 수 있는 권한이 없습니다. |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->