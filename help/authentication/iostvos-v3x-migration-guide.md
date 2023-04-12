---
title: iOS/tvOS v3.x 마이그레이션 안내서
description: iOS/tvOS v3.x 마이그레이션 안내서
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# iOS/tvOS v3.x 마이그레이션 안내서 {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

>[!TIP]
> 
> **참고:**
>
> - iOS sdk 버전 3.1부터 구현자는 이제 WKWebView 또는 UIWebView를 서로 교환하여 사용할 수 있습니다. UIWebView는 더 이상 사용되지 않으므로 앱은 향후 iOS 버전에 대한 문제를 방지하기 위해 WKWebView로 마이그레이션해야 합니다.
> - 마이그레이션은 WKWebView를 사용하여 UIWebView 클래스를 단순히 전환하는 것을 의미하며, Adobe의 AccessEnabler에 대해 수행할 특정 작업은 없습니다.


</br>

## 빌드 설정 업데이트 {#update}

이 릴리스에는 SWIFT 언어로 작성된 기능이 포함되어 있습니다. 앱이 완전히 Objective-C인 경우 Target의 빌드 설정에서 &quot;Always Embed Swift Standard Libraries&quot; 확인란을 &quot;Yes&quot;로 설정해야 합니다. 이 옵션이 설정되면 Xcode는 앱에서 번들 프레임워크를 검색하고, 프레임워크에 Swift 코드가 포함되어 있으면 해당 라이브러리를 앱 번들에 복사합니다. 빌드 설정을 업데이트하지 않으면 AccessEnabler.framework 또는 여러 가지 파일을 로드할 수 없다는 오류 때문에 앱이 충돌할 수 있습니다 `ibswift*` 라이브러리.

</br>

## 소프트웨어 명세서 추가 {#add}

> 소프트웨어 명세서를 가져오는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오
> 페이지:
> [애플리케이션 등록](/help/authentication/iostvos-application-registration.md)

소프트웨어 구문을 보유하고 나면 App Store에서 새로운 버전의 응용 프로그램을 배포하지 않고도 쉽게 취소하거나 변경할 수 있도록 원격 서버에서 호스팅하는 것이 좋습니다. 애플리케이션이 시작되면 원격 위치에서 소프트웨어 문을 가져와 AccessEnabler 생성자에 전달합니다.

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> API 정보는 다음과 같습니다. [iOS / tvOS API 참조](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 사용자 지정 URL 체계 추가 {#add-custom}

> 사용자 지정 URL 체계를 가져오는 방법에 대한 자세한 내용은 다음 페이지로 이동하십시오. [고객 URL 체계 가져오기](/help/authentication/iostvos-application-registration.md)

사용자 지정 URL 체계를 가져온 후에는 해당 URL을 애플리케이션의 info.plist 파일에 추가해야 합니다. 사용자 지정 구성표의 형식은 다음과 같습니다. `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. 파일에 추가할 때 콜론과 슬래시를 생략해야 합니다. 위의 예제는 `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>
```

</br>

## 사용자 지정 URL 체계에서 호출 차단 {#intercept}

이는 애플리케이션이 이전에 를 통해 Safari View Controller(SVC) 처리를 활성화한 경우에만 적용됩니다. [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) SVC(Safari View Controller)가 필요한 특정 MVPD에 대해 및 를 호출하므로 UIWebView/WKWebView 컨트롤러 대신 SFSsafariViewController에서 인증 및 로그아웃 끝점을 로드해야 합니다.

인증 및 로그아웃 흐름 중에 응용 프로그램은 `SFSafariViewController `여러 리디렉션을 거칠 때 제어하십시오. 애플리케이션이 사용자가 정의한 특정 사용자 지정 URL을 로드하는 때를 감지해야 합니다 `application's custom URL scheme` (예:`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. 컨트롤러가 이 특정 사용자 지정 URL을 로드하면 애플리케이션이 `SFSafariViewController` AccessEnabler를 호출하고 `handleExternalURL:url `API 메서드.

사용자 `AppDelegate` 다음 메서드를 추가합니다.

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> API 정보는 다음과 같습니다. [외부 URL 처리](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## setRequestor 메서드 서명 업데이트 {#update-setreq}

새 SDK는 새 인증 메커니즘을 사용하므로 signedRequestId 매개 변수 또는 공개 키 및 암호(tvOS용)가 필요하지 않습니다. 다음 `setRequestor` 메서드가 단순화되고 requestorID만 필요합니다.

### iOS

이 코드:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

다음과 같이 바꿉니다.

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

이 코드:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

다음과 같이 바꿉니다.

```swift
    accessEnabler.setRequestor(requestorId)
```

> API 정보는 다음과 같습니다. [요청자 설정](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## getAuthenticationToken 메서드를 handleExternalURL 메서드로 바꿉니다 {#replace}

`getAuthentication` 메서드는 과거에 인증 흐름을 완료하는 데 사용되었습니다. 이름이 오해되었기 때문에 `handleExternalURL` 및 은 url을 매개 변수로 사용합니다.

다음 항목의 모든 항목 변경:

```swift
    accessEnabler.getAuthenticationToken()
```

아래와 같이 변경하는 것을 의미합니다.

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> API 정보는 다음과 같습니다. [외부 URL 처리](/help/authentication/iostvos-sdk-api-reference.md)
