---
title: 로그아웃 시작
description: 로그아웃 시작
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 로그아웃 시작 {#initiate-logout}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## REST API 엔드포인트 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## 설명 {#description}

저장소에서 AuthN 및 AuthZ 토큰을 제거합니다.


| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/logout | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자</br>2.  deviceId(필수)</br>3.  device_info/X-Device-Info(필수)</br>4.  _deviceType_</br> 5.  _deviceUser_ (더 이상 사용되지 않음)</br>6.  _appId_ (더 이상 사용되지 않음) | DELETE | 없음 | 204 |


| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보.</br></br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br></br>자세한 내용은 [통과 지표에서 clientless 장치 유형 매개 변수를 사용하는 것의 이점&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다.</br></br>**참고**: 를 사용하는 경우 deviceUser는 와 동일한 값을 가져야 합니다 [등록 코드 만들기](/help/authentication/registration-code-request.md) 요청. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info는 이 매개 변수를 대체합니다. 사용하는 경우, `appId` 에는 와 동일한 값이 있어야 합니다. [등록 코드 만들기](/help/authentication/registration-code-request.md) 요청. |

>[!IMPORTANT]
> 
>현재 로그아웃 호출에는 다음과 같은 제한이 있습니다. AuthN 및 AuthZ 토큰을 스토리지(예: Programmer / Primetime 인증 측)에서 지우지만 **포함하지 않음** mvpd 로그아웃 끝점을 호출합니다. 


