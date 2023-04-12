---
title: 클라이언트 정보 전달(장치, 연결 및 응용 프로그램)
description: 클라이언트 정보 전달(장치, 연결 및 응용 프로그램)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---


# 클라이언트 정보 전달(장치, 연결 및 응용 프로그램) {#pass-client-info}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.


## 범위 {#pass-client-info-scope}

이 문서는 Programmer 애플리케이션에서 Adobe Primetime Authentication REST API 또는 SDK로 클라이언트 정보(장치, 연결 및 애플리케이션)를 전달하는 세부 정보 및 Cookbook을 집계합니다.

클라이언트 정보를 제공하면 다음과 같은 이점이 있습니다.

* HBA를 지원할 수 있는 일부 디바이스 유형 및 MVPD의 경우 HBA(홈 베이스 인증)를 올바르게 활성화할 수 있습니다.
* 일부 장치 유형의 경우 TTL을 올바르게 적용할 수 있는 기능(예: TV에 연결된 장치의 인증 세션에 대해 긴 TTL을 구성).
* ESM(Entitlement Service Monitoring)을 사용하여 장치 유형 간에 분류된 보고서에서 비즈니스 지표를 적절히 집계하는 기능.
* 다양한 비즈니스 규칙을 적절하게 적용하는 기능을 차단합니다(예: 성능 저하)가 발생합니다.

## 개요 {#pass-client-info-overview}

클라이언트 정보는 다음과 같이 구성됩니다.

* **장치** 사용자가 프로그래머 콘텐츠를 소비하려고 하는 장치의 하드웨어 및 소프트웨어 특성에 대한 정보입니다.
* **연결** 사용자가 Adobe Primetime 인증 서비스 및/또는 프로그래머 서비스(예: 서버 간 구현)에 연결하는 장치의 연결 속성에 대한 정보입니다.
* **애플리케이션** 사용자가 Programmer 콘텐츠를 소비하려고 하는 곳에서 등록된 응용 프로그램에 대한 정보입니다.

클라이언트 정보는 다음 표에 나와 있는 키가 포함된 JSON 개체입니다.

>[!NOTE]
>
>다음 **키** is **필수** 클라이언트 정보 JSON 개체에 전송하려면 다음을 수행하십시오. **모델**, **osName**.
>
>다음 키에는 **제한** 값: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | 키 | 제한됨 | 설명 | 가능한 값 |
|---|---|---|---|---|
|  | primaryHardwareType | # 예 | 장치의 기본 하드웨어 유형입니다. | # 값이 제한됩니다. 카메라 데이터 수집터미널 데스크탑 임베디드 네트워크 모듈 eReader 게임GeolocationTracker Glass MediaPlayer 모바일Phone 결제터미널 플러그인Modem SetTopBox TV Tablet WirelessHotspot Watch 알 수 없음 |
| #mandatory | 모델 | 아니요 | 장치의 모델 이름입니다. | 예: iPhone, SM-G930V, AppleTV 등 |
|  | 버전 | 아니요 | 장치의 버전입니다. | 예: 2.0.1 등 |
|  | 제조업체 | 아니요 | 장치의 제조 회사/조직. | 예: 삼성, LG, ZTE, 화웨이, 모토로라, Apple 등 |
|  | 공급업체 | 아니요 | 장치의 판매 회사/조직. | 예: Apple, 삼성, LG, Google 등 |
| #mandatory | osName | # 예 | 장치의 운영 체제(OS) 이름입니다. | # 값이 제한됩니다. Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | 예 | 장치의 OS(운영 체제) 그룹 이름입니다. | # 값이 제한됩니다. Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | 아니요 | 장치의 OS(운영 체제) 공급자입니다. | Amazon Apple Google LG Microsoft Mozilla Nintendo Roku 삼성 Sony Titen Project |
|  | osVersion | 아니요 | 장치의 OS(운영 체제) 버전입니다. | 예: 10.2, 9.0.1 등 |
|  | browserName | # 예 | 브라우저의 이름입니다. | # 값이 제한됩니다. Android Browser Chrome Edge Firefox Internet Explorer Opera Safari SeaMuno Symbian Browser |
|  | browserVendor | # 예 | 브라우저의 빌딩 회사/조직입니다. | # 값이 제한됩니다. Amazon Apple Google Microsoft 모토로라 Mozilla Netscape Nintendo Nokia Sony Ericsson |
|  | browserVersion | 아니요 | 장치의 브라우저 버전입니다. | 예: 60.0.3112 |
|  | userAgent | 아니요 | 장치의 사용자 에이전트입니다. | 예: Mozilla/5.0(Macintosh) 인텔 Mac OS X 10_12_3) AppleWebKit/602.4.8(Gecko와 같은 KHTML) 버전/10.0.3 Safari/602.4.8 |
|  | displayWidth | 아니요 | 장치의 실제 화면 너비입니다. |  |
|  | displayHeight | 아니요 | 장치의 실제 화면 높이입니다. |  |
|  | displayPpi | 아니요 | 장치의 실제 화면 픽셀 밀도입니다. | 예: 294 |
|  | diagonalScreenSize | 아니요 | 장치의 실제 화면 대각선 차원(인치)입니다. | 예: 5.5, 10.1 |
|  | connectionIp | 아니요 | HTTP 요청 전송에 사용되는 장치의 IP입니다. | 예: 8.8.4.4 |
|  | connectionPort | 아니요 | HTTP 요청을 전송하는 데 사용되는 장치의 포트입니다. | 예: 53124 |
|  | connectionType | 아니요 | 네트워크 연결 유형입니다. | 예: WiFi, LAN, 3G, 4G, 5G |
|  | connectionSecure | # 예 | 네트워크 연결 보안 상태입니다. | # 값이 제한됩니다. true - 보안 네트워크의 경우 false - 공용 핫픽스의 경우 |
|  | applicationId | 아니요 | 애플리케이션의 고유 식별자입니다. | 예: CNN |

## API 참조 {#api-ref}

이 섹션에서는 Adobe Primetime 인증 REST API 또는 SDK를 사용할 때 클라이언트 정보를 처리할 책임이 있는 API를 제공합니다.

### REST API {#rest-api}

Adobe Primetime 인증 서비스는 다음과 같은 방법으로 클라이언트 정보를 수신합니다.

* 로서의 **헤더: &quot;X-Device-Info&quot;**
* 로서의 **쿼리 매개 변수: &quot;device_info&quot;**
* 로서의 **post 매개 변수: &quot;device_info&quot;**

>[!IMPORTANT]
>
>세 가지 시나리오 모두에서 헤더나 매개 변수의 페이로드는 **Base64 인코딩 및 URL 인코딩**.

**SDK**

#### JavaScript SDK {#js-sdk}

AccessEnabler JavaScript SDK는 기본적으로 재정의되지 않은 한 Adobe Primetime 인증 서비스로 전달되는 클라이언트 정보 JSON 개체를 빌드합니다.

AccessEnabler JavaScript SDK는 **재정의 전용** 클라이언트 정보 JSON 개체의 &quot;applicationId&quot; 키가 [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))s *applicationId* options 매개 변수입니다.

>[!CAUTION]
>
>다음 `applicationId` 매개 변수 값은 일반 텍스트 문자열 값이어야 합니다.
>프로그래머 애플리케이션에서 applicationId를 전달하기로 결정한 경우 나머지 클라이언트 정보 키는 AccessEnabler JavaScript SDK에 의해 계속 계산됩니다.

#### iOS/tvOS SDK {#ios-tvos-sdk}

AccessEnabler iOS/tvOS SDK는 기본적으로 재정의되지 않는 한 Adobe Primetime 인증 서비스로 전달되는 클라이언트 정보 JSON 개체를 빌드합니다.

AccessEnabler iOS/tvOS SDK는 **전체 무시** 를 통해 클라이언트 정보 JSON 개체 [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)&#39;s device_info 매개 변수.

>[!CAUTION]
>
>다음 *device_info* 매개 변수 값은 여야 합니다. **Base64 인코딩** *NSString* 값.
>
>Programmer 응용 프로그램이 *device_info*&#x200B;를 입력하면 AccessEnabler iOS/tvOS SDK에서 계산된 모든 클라이언트 정보 키가 재정의됩니다. 따라서 가능한 한 많은 키의 값을 계산하고 전달하는 것이 매우 중요합니다. 구현에 대한 자세한 내용은 [개요](#pass-client-info-overview) 테이블 및 [iOS/tvOS Cookbook](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

다음 `AccessEnabler` Android/FireOS SDK는 기본적으로 재정의되지 않는 한 Adobe Primetime 인증 서비스로 전달되는 클라이언트 정보 JSON 개체를 빌드합니다.

다음 `AccessEnabler` Android/FireOS SDK가 지원 **전체 무시** 를 통해 클라이언트 정보 JSON 개체 [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)&#39;s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)s `device_info` 매개 변수.

>[!NOTE]
>
>다음 `device_info` 매개 변수 값은 여야 합니다. **Base64 인코딩** 문자열 값.

>[!IMPORTANT]
>
>Programmer 응용 프로그램이 `device_info`를 입력한 다음 `AccessEnabler` Android/FireOS SDK가 재정의됩니다. 따라서 가능한 한 많은 키의 값을 계산하고 전달하는 것이 매우 중요합니다. 구현에 대한 자세한 내용은 [개요](#pass-client-info-overview) 테이블 및 [Android](#android) 및 [FireOS](#fire-tv) 요리책.

## 요리책 {#cookbooks}

이 섹션에서는 다양한 장치 유형의 경우 클라이언트 정보 JSON 개체를 작성하는 Cookbook에 대해 설명합니다.

>[!IMPORTANT]
>
>로 표시된 키  **!** 전송해야 합니다.

### Android {#android}

장치 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---------------|-----------------------------|---------------|
| ! | 모델 | Build.MODEL | GT-I9505 |
|  | 공급업체 | Build.BRAND | 삼성 |
|  | 제조업체 | Build.MANUFACTURER | 삼성 |
| ! | 버전 | Build.DEVICE | jflte |
|  | displayWidth | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | 하드코딩된 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

연결 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

애플리케이션 정보는 다음과 같은 방식으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---------------|-----------|--------------|
|  | applicationId | 하드코딩된 | CNN |

>[!IMPORTANT]
장치, 연결 및 애플리케이션 정보를 동일한 JSON 개체에 추가해야 합니다. 그런 다음 결과 개체가 **Base64 인코딩**. 또한 Adobe Primetime 인증 REST API의 경우 값은 **URL 인코딩**.

**샘플 코드**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
**리소스:**
* 공용 클래스 [빌드](https://developer.android.com/reference/android/os/Build.html){target=_blank} ( Java 개발자 설명서).


### FireTV {#fire-tv}

장치 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예:) |
|---|---------------|-----------------------------|--------------|
| ! | 모델 | Build.MODEL | AFTM |
|  | 공급업체 | Build.BRAND | Amazon |
|  | 제조업체 | Build.MANUFACTURER | Amazon |
| ! | 버전 | Build.DEVICE | 몬토야 |
|  | displayWidth | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | 하드코딩된 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

연결 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

애플리케이션 정보는 다음과 같은 방식으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---------------|-----------|--------------|
|  | applicationId | 하드코딩된 | CNN |

>[!IMPORTANT]
장치, 연결 및 애플리케이션 정보를 동일한 JSON 개체에 추가해야 합니다. 그런 다음 결과 개체가 **Base64 인코딩**. 또한 Adobe Primetime 인증 REST API의 경우 값은 **URL 인코딩**.

>[!NOTE]
**리소스:**
* 공용 클래스 [빌드](https://developer.android.com/reference/android/os/Build.html){target=_blank} ( Android 개발자 설명서).
* [FireTV 장치 식별](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

장치 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---------------|------------------------|--------------|
| ! | 모델 | uname.machine | iPhone |
|  | 공급업체 | 하드코딩된 | Apple |
|  | 제조업체 | 하드코딩된 | Apple |
| ! | 버전 | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

연결 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [Reachability currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


애플리케이션 정보는 다음과 같은 방식으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---------------|-----------|--------------|
|  | applicationId | 하드코딩된 | CNN |

>[!IMPORTANT]
장치, 연결 및 애플리케이션 정보를 동일한 JSON 개체에 추가해야 합니다. 그런 다음 결과 개체가 Base64로 인코딩되어야 합니다. 또한 Adobe Primetime 인증 REST API의 경우 값을 URL로 인코딩해야 합니다.

**샘플 코드**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
**리소스:**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [이름 없음](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [연결 가능성 정보](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

장치 정보는 다음과 같은 방법으로 작성할 수 있습니다.

| 키 | 소스 | 값(예) |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | 모델 | 하드코딩된 | &quot;Roku&quot; |
|  | 공급업체 | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
|  | 제조업체 | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
| ! | 버전 | ifDeviceInfo.GetModelDetails().ModelNumber | &quot;5303X&quot; |
|  | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | 하드코딩된 | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

연결 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;, &quot;WifiConnection&quot; |
|  | connectionSecure | 하드코딩된 | 연결이 연결되어 있는 경우 true |

애플리케이션 정보는 다음과 같은 방식으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---------------|-----------|--------------|
|  | applicationId | 하드코딩된 | CNN |

>[!IMPORTANT]
장치, 연결 및 애플리케이션 정보를 동일한 JSON 개체에 추가해야 합니다. 그런 다음 결과 개체가 **Base64 인코딩**. 또한 Adobe Primetime 인증 REST API의 경우 값을 URL로 인코딩해야 합니다.

>[!NOTE]
자세한 내용은 [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

장치 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 값(예) |
|---|---|---|---|
| ! | 모델 | EasClientDeviceInformation.SystemProductName |  |
|  | 공급업체 | 하드코딩된 | Microsoft |
|  | 제조업체 | 하드코딩된 | Microsoft |
| ! | 버전 | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

연결 정보는 다음과 같은 방법으로 작성할 수 있습니다.

|  | 키 | 소스 | 예 |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | NetworkAuthenticationType | &quot;없음&quot;, &quot;Wpa&quot; 등 |

애플리케이션 정보는 다음과 같은 방식으로 작성할 수 있습니다.

| 키 | 소스 | 값(예) |
|---|---|---|
| applicationId | 하드코딩된 | CNN |

>[!IMPORTANT]
장치, 연결 및 애플리케이션 정보를 동일한 JSON 개체에 추가해야 합니다. 그런 다음 결과 개체가 **Base64 인코딩**. 또한 Adobe Primetime 인증 REST API의 경우 값은 **URL 인코딩**.

**리소스**

* [EasClientDeviceInformation 클래스](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [DisplayInformation 클래스](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)


