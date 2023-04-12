---
title: iOS SDK 3.2 이상에서 SFSsafariViewController 지원
description: iOS SDK 3.2 이상에서 SFSsafariViewController 지원
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# iOS SDK 3.2 이상에서 SFSsafariViewController 지원 {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>


**보안 요구 사항으로 인해 일부 MVPD의 로그인 페이지가 웹 보기가 아닌 SFSsafariViewController에 표시되어야 합니다.**

일부 MVPD는 로그인 페이지를 SFSsafariViewController와 같은 보안 브라우저 컨트롤에 표시해야 합니다. 웹 뷰를 적극적으로 차단하므로 인증하려면 SVC를 사용해야 합니다. 

## 호환성 {#compatiblity}

iOS SDK 버전 3.1부터 AccessEnabler SDK는 서버 구성에 따라 SFSsafariViewController에서 특정 MVPD에 대한 로그인 페이지를 자동으로 표시합니다.

SDK 버전 3.1은 응용 프로그램의 루트 보기 컨트롤러에서 SFSsafariViewController를 자동으로 표시합니다. 이렇게 하면 구현자에 대한 로그인 페이지 관리를 간소화할 수 있지만, 앱의 특정 구현(예: 이미 표시된 모달 컨트롤러)으로 인해 루트 보기 컨트롤러에서 SFSsafariViewController를 표시할 수 없는 경우가 있습니다.

이와 같은 경우 3.2 버전에서는 프로그래머가 SVC를 수동으로 관리할 수 있는 기능을 도입했습니다.

## 수동 SVC 관리 {#manual-svc-management}

SVC를 수동으로 관리하려면 구현자가 다음 단계를 수행해야 합니다.
 

1. 호출 **setOptions([&quot;handleSVC&quot;:true])** AccessEnabler 초기화 후 인증을 시작하기 전에 이 호출이 수행되었는지 확인합니다. 이를 통해 &quot;수동&quot; SVC 관리를 수행할 수 있으며 SDK가 SVC를 자동으로 제공하지 않고, 필요할 때 SVC를 호출하게 됩니다 **navigate(toUrl:*{url}* useSVC:true)**.  

1. 선택적 콜백 구현 **navigateToUrl:useSVC:** 구현 내에서 제공된 url을 사용하여 svc 인스턴스를 만들고 화면에 표시해야 합니다.

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***참고:***

   - *원하는 방식으로 SFSsafariViewController를 사용자 지정할 수 있습니다. 예를 들어 iOS 11+에서 &quot;완료&quot; 레이블을 &quot;취소&quot;로 변경할 수 있습니다.*
   - *svc를 해지하려면 해당 서비스에 대한 참조가 필요합니다. 서비스 범위에 해당 서비스를 만들지 마십시오 **navigateToUrl:useSVC***
   - *&quot;myController&quot;에 대해 고유한 보기 컨트롤러 사용*\
       

1. 애플리케이션의 위임 구현에서 **application(\_app: UIApplication, open url: URL, 옵션: \[UIApplicationOpenURLOptionsKey: Any\]) -\> 부울**&#x200B;를 눌러 svc를 닫기 위해 코드를 추가합니다. 거기에 이미 를 호출하는 코드가 있어야 합니다 **accessEnabler.handleExternalURL()**. 바로 아래에 추가:

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   또한 svc 는 2단계에서 작성한 SFSsafariViewController에 대한 참조입니다.\
    

1. 구현 **safariViewControllerDidFinish(\_ 컨트롤러: SFSsafariViewController)** 변환 전: **SFSsafariViewControllerDelegate** 사용자가 &quot;완료&quot; 버튼을 사용하여 svc를 취소한 경우를 포착하기 위해 이 함수에서 인증이 취소되었음을 SDK에 알려면 다음을 호출해야 합니다.

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```

