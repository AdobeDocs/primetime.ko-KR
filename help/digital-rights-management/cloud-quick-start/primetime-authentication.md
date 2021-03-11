---
title: Adobe Primetime 인증(선택 사항)
description: Adobe Primetime 인증(선택 사항)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Adobe Primetime 인증(선택 사항) {#adobe-primetime-authentication-optional}

콘텐츠를 패키징하는 데 사용되는 DRM 정책이 익명 정책이면 모든 라이선스 요청에 라이센스가 부여됩니다. 또한 Primetime Cloud DRM은 Adobe Primetime 인증을 통한 인증도 지원합니다. 이 기능이 활성화되어 있으면 클라이언트 장치가 Primetime 인증 토큰을 처음 취득하여 사용자 정의 인증 토큰을 설정하기 위한 적절한 클라이언트 API( `setAuthenticationToken`)를 통해 로컬로 설정하지 않으면 라이센스가 발행되지 않습니다. Primetime 인증을 인증 워크플로우에 통합하는 방법에 대한 자세한 내용은 다음을 참조하십시오.[Adobe Primetime 인증](https://tve.helpdocsonline.com/home)

라이센스 취득 과정에서 DRM 정책에 Pri Metime 인증이 필요하다고 명시되어 있는 경우 라이선스 서버는 Primetime 인증 Short Media Token을 구문 분석하고 확인합니다. DRM 정책이 `ResourceID` 또는 `RequestorID`을 지정하는 경우 라이선스 서버도 이러한 속성에 대해 토큰의 유효성을 확인합니다. 설정이 되어 있지 않으면 토큰 유효성 검사 중에 라이센스 서버에서 속성을 &quot;null&quot;로 지정합니다. 토큰 유효성 검사가 성공한 경우에만 라이센스가 발급됩니다.그렇지 않으면 클라이언트에서 305 하위 오류 코드(사용자 권한 없음)가 포함된 3328 DRMErrorEvent를 전달합니다.

Primetime 인증을 필요로 하는 콘텐츠를 패키징하는 데 사용되는 정책에 Primetime 인증 매개 변수가 포함되어야 합니다.

관련 속성은 다음과 같습니다.

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>(DRM) 라이선스 순환 기능과 함께 Primetime 인증을 사용하는 경우 Primetime 인증 SMT(Short Media Token)의 유효 기간이 짧습니다. 응용 프로그램이 라이센스 순환 사용을 사용할 계획인 경우(예: *Blading* 사용 사례), 응용 프로그램은 라이센스를 회전하기 전에 이러한 사항을 인식하고 Primetime 인증 짧은 미디어 토큰을 새로 고쳐야 합니다.