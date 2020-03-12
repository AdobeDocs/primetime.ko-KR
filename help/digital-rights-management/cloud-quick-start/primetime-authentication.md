---
seo-title: Adobe Primetime 인증(옵션)
title: Adobe Primetime 인증(옵션)
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime 인증(옵션) {#adobe-primetime-authentication-optional}

컨텐츠를 패키지하는 데 사용되는 DRM 정책이 익명 정책이면 모든 라이센스 요청에 라이센스가 부여됩니다. 또한 Primetime Cloud DRM은 Adobe Primetime 인증을 통한 인증을 지원합니다. 이 기능이 활성화되면 클라이언트 장치가 Primetime 인증 토큰을 처음 취득하여 사용자 정의 인증 토큰을 설정하기 위해 적절한 클라이언트 API( `setAuthenticationToken`)를 통해 로컬로 설정하지 않으면 라이센스가 발행되지 않습니다. Primetime 인증을 인증 워크플로우에 통합하는 방법에 대한 자세한 내용은 다음을 참조하십시오.Adobe [Primetime 인증](https://tve.helpdocsonline.com/home)

라이센스 취득 동안 DRM 정책에 Pri Metime 인증이 필요하다고 명시되어 있는 경우 라이선스 서버는 Primetime 인증 Short Media Token을 구문 분석하여 확인합니다. DRM 정책이 `ResourceID` 또는 를 지정하는 `RequestorID`경우 라이선스 서버도 해당 속성에 대해 토큰의 유효성을 확인합니다. 이 속성이 설정되지 않은 경우, 라이선스 서버는 토큰 유효성 검사 동안 속성을 &quot;null&quot;로 지정합니다. 토큰 유효성 검사가 성공한 경우에만 라이센스가 발급됩니다.그렇지 않으면 클라이언트가 305 하위 오류 코드(권한 없음)가 있는 3328 DRMErrorEvent를 전달합니다.

Primetime 인증이 필요한 콘텐츠를 패키징하는 데 사용되는 정책에 Primetime 인증 매개 변수가 지정되어 있어야 합니다.

관련 속성은 다음과 같습니다.

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>DRM(Primetime) 라이선스 순환 기능과 함께 Primetime 인증을 사용하는 경우 Primetime 인증 SMT(Short Media Token)의 유효 기간이 짧다는 점을 유의하십시오. 애플리케이션이 라이선스 순환(예: 일시 중단 사용 *사례* 지원)을 사용하려는 경우, 애플리케이션을 전환하기 전에 이를 알고 Primetime 인증 짧은 미디어 토큰을 새로 고쳐야 합니다.