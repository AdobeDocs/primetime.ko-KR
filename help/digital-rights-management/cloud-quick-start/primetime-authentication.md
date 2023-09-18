---
title: Adobe Primetime 인증(선택 사항)
description: Adobe Primetime 인증(선택 사항)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Adobe Primetime 인증(선택 사항) {#adobe-primetime-authentication-optional}

콘텐츠를 패키지하는 데 사용되는 DRM 정책이 익명 정책인 경우 모든 라이선스 요청에 라이선스가 발급됩니다. 선택적으로 Primetime Cloud DRM도 Adobe Primetime 인증을 통한 인증을 지원합니다. 이 기능이 활성화되어 있으면 클라이언트 장치가 먼저 Primetime 인증 토큰을 획득하고 적절한 클라이언트 API( 를 통해 로컬로 설정하지 않으면 라이센스가 발행되지 않습니다. `setAuthenticationToken`사용자 지정 인증 토큰을 설정합니다. Primetime 인증을 인증 워크플로에 통합하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [Adobe Primetime 인증.](https://tve.helpdocsonline.com/home)

라이센스 획득 중에 DRM 정책이 Pri Metime 인증이 필요함을 나타내는 경우 라이센스 서버는 Primetime 인증 Short Media 토큰을 구문 분석하고 유효성을 검사합니다. DRM 정책이 `ResourceID` 또는 `RequestorID`를 입력하면 라이센스 서버에서도 이러한 속성에 대해 토큰의 유효성을 검사합니다. 설정되지 않은 경우 라이선스 서버는 토큰 유효성 검사 중에 속성을 &quot;null&quot;로 지정합니다. 토큰 유효성 검사에 성공해야 라이선스가 발급됩니다. 그렇지 않으면 305 하위 오류 코드(사용자가 승인되지 않음)가 있는 3328 DRMErrorEvent가 클라이언트에 의해 발송됩니다.

Primetime 인증이 필요한 콘텐츠를 패키징하는 데 사용되는 정책에 Primetime 인증 매개 변수를 지정해야 합니다.

관련 속성은 다음과 같습니다.

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Primetime 인증을 (DRM) 라이선스 회전 기능과 함께 사용할 때는 Primetime 인증 SMT(Short Media Token)의 유효일이 짧다는 점을 유의하십시오. 애플리케이션이 라이센스 회전을 사용할 계획인 경우(예: *일시 중단* 사용 사례)를 사용하면 애플리케이션에서 이를 인식하고 라이선스를 회전하기 전에 Primetime 인증 Short Media 토큰을 새로 고쳐야 합니다.
