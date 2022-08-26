---
title: 사용자 메타데이터
description: 사용자 메타데이터
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# 사용자 메타데이터 {#user-metadata}

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

MVPD가 인증된 사용자에 대해 공유한 메타데이터를 검색합니다.

<div>


| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자</br>2.  deviceId(필수)</br>3.  device_info/X-Device-Info(필수)</br>4.  deviceType</br>5.  deviceUser(사용 중지)</br>6.  appId(더 이상 사용되지 않음) | GET | 실패한 경우 사용자 메타데이터 또는 오류 세부 정보가 포함된 XML 또는 JSON입니다. | 200 - 성공</br></br>404 - 메타데이터가 없습니다.</br></br>412 - 잘못된 AuthN 토큰(예: 만료된 토큰) |


| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보.</br></br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br>자세한 내용은 [장치 및 연결 정보 전달](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다.</br></br>**참고**: 를 사용하는 경우 deviceUser는 와 동일한 값을 가져야 합니다 [등록 코드 만들기](http://tve.helpdocsonline.com/registration-code-request) 요청. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info는 이 매개 변수를 대체합니다. 사용하는 경우, `appId` 에는 와 동일한 값이 있어야 합니다. [등록 코드 만들기](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) 요청. |

>[!NOTE]
> 
>인증 흐름이 완료된 후에 사용자 메타데이터 정보를 사용할 수 있어야 하지만, MVPD 및 메타데이터 유형에 따라 인증 플로우에서 업데이트할 수 있습니다.

</br>

## 샘플 응답 {#sample-response}

호출이 성공하면 서버가 아래 표시된 것과 유사한 구조로 XML(기본값) 또는 JSON 개체로 응답합니다.

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
              },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
    }
```

 

객체 루트에 세 개의 노드가 있습니다.

* *업데이트됨*: 메타데이터가 마지막으로 업데이트된 시간을 나타내는 UNIX 타임스탬프를 지정합니다. 이 속성은 인증 단계 동안 메타데이터를 생성할 때 서버가 처음에 설정합니다. 이후 호출(메타데이터가 업데이트된 후)에서는 타임스탬프가 증가합니다.

* *데이터*: 에 실제 메타데이터 값이 포함되어 있습니다. 

* *암호화된*: 암호화된 속성을 나열하는 배열입니다. 특정 메타데이터 값을 해독하려면 Programmer에서 메타데이터에 대해 Base64 디코딩을 수행한 다음 자체 개인 키를 사용하여 결과 값에 RSA 암호 해독을 적용해야 합니다(Adobe은 Programmer의 공개 인증서를 사용하여 서버의 메타데이터를 암호화합니다).

오류가 발생하면 서버가 세부 오류 메시지를 지정하는 XML 또는 JSON 개체를 반환합니다.

**추가 정보:** [사용자 메타데이터](http://tve.helpdocsonline.com/user-metadata-v2)


### [REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
