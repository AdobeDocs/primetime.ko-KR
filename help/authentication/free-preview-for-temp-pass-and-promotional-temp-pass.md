---
title: 임시 통과 및 프로모션 임시 패스에 대한 무료 미리 보기
description: 임시 통과 및 프로모션 임시 패스에 대한 무료 미리 보기
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# 임시 통과 및 프로모션 임시 패스에 대한 무료 미리 보기 {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

두 번째 화면 없이 임시 통과 및 프로모션 임시 패스에 대한 인증 토큰을 만들 수 있습니다.


| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. requestor_id(필수)</br>    </br>2.  deviceId(필수)</br>    </br>3.  mso_id(필수)</br>    </br>4.  domain_name(필수)</br>    </br>5.  device_info/X-Device-Info(필수)</br>6.  deviceType</br>    </br>7.  deviceUser(사용 중지)</br>    </br>8.  appId(더 이상 사용되지 않음)</br>    </br>9.  generic_data(선택 사항) | POST | 성공적인 응답은 토큰이 성공적으로 만들어졌고 인증 흐름에 사용할 준비가 되었음을 나타내는 204 컨텐츠 없음이 됩니다. | 204 - 컨텐츠 없음   </br>400 - 잘못된 요청 |

<div>


| 입력 매개 변수 | 설명 |
| --- | --- |
| requestor_id | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| mso_id | 이 작업이 유효한 MVPD ID입니다. |
| domain_name | 토큰이 부여될 도메인 이름입니다. 인증 토큰이 부여될 때 서비스 공급자의 도메인과 비교됩니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보.</br></br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br></br>자세한 내용은 [클라이언트 없는 장치 유형 매개 변수를 사용하는 이점&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다.</br></br>**참고**: 를 사용하는 경우 deviceUser는 와 동일한 값을 가져야 합니다 [등록 코드 만들기](/help/authentication/registration-code-request.md) 요청. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info는 이 매개 변수를 대체합니다. 사용하는 경우, `appId` 에는 와 동일한 값이 있어야 합니다. [등록 코드 만들기](/help/authentication/registration-code-request.md) 요청. |
| generic_data | 프로모션 임시 패스에 대한 토큰 범위를 제한하는 데 사용됩니다. |


### [REST API 참조로 돌아가기](/help/authentication/rest-api-reference.md)
