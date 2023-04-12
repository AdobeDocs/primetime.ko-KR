---
title: iOS 인증 오류 - adobepass.ios.app을 찾을 수 없음
description: iOS 인증 오류 - adobepass.ios.app을 찾을 수 없음
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# iOS 인증 오류 - adobepass.ios.app을 찾을 수 없음 {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 문제 {#issue}

사용자가 인증 플로우를 통과하고, 공급자와 함께 자격 증명을 성공적으로 입력하면 오류 페이지, 검색 페이지 또는 사용자에게 이를 알리는 일부 다른 사용자 지정 페이지로 다시 리디렉션됩니다 `adobepass.ios.app` 찾을 수 없거나 확인할 수 없습니다.

## 설명 {#explanation}

iOS에서 `adobepass.ios.app` AuthN 플로우가 완료되었음을 나타내는 최종 리디렉션 URL로 사용됩니다. 이 시점에서 AuthN 토큰을 가져오고 AuthN 흐름을 확정하려면 AccessEnabler에 요청을 해야 합니다.

문제는 `adobepass.ios.app` 은 실제로 존재하지 않으며 의 `webView`. 이전 버전의 iOS DemoApp에서는 이 오류가 항상 AuthN 흐름 끝에서 트리거된다고 가정하고 이를 적절하게 처리하도록 설정했습니다(`indidFailLoadWithError`).

**참고:** 이 문제는 이후 버전의 DemoApp(iOS SDK 다운로드에 포함)에서 해결되었습니다.

불행히도, 이 가정은 옳지 않다. 소위 &quot;스마트&quot; DNS 또는 프록시 서버로서, 발생한 오류를 단순히 전달하지 않고 대신 다음 중 하나를 수행합니다. 

- 사용자 지정 오류 페이지 만들기
- 검색 페이지, 기타 유형의 고객 페이지 또는 포털로 이동합니다.

이러한 경우 iOS webView로 돌아가는 응답은 webView에 대한 한 완벽하게 유효한 응답이며 이전 DemoApp이 종속했던 오류를 트리거하지 않습니다.

## 솔루션 {#solution}

DemoApp이 수행하는 것과 동일한 가정을 하지 마십시오. 대신 가 실행되기 전에 요청을 가로채십시오( `shouldStartLoadWithRequest`)을 사용하여 적절하게 처리할 수 있습니다.

요청이 실행되기 전에 요청을 가로채는 방법의 예:

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

몇 가지 주목할 사항이 있습니다.

- 사용 안 함 `adobepass.ios.app` 코드에서 바로 그 위치에 있습니다. 대신 상수를 사용하십시오 `ADOBEPASS_REDIRECT_URL`
- 다음 `return NO;` 문에서 페이지를 로드할 수 없습니다.
- 반드시 `getAuthenticationToken` 호출은 코드에서 한 번 호출되고 한 번만 호출됩니다. 에 대한 여러 호출 `getAuthenticationToken` 결과는 정의되지 않은 결과를 생성합니다.

