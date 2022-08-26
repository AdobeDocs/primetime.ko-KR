---
title: 인증 시작
description: 인증 시작
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# 인증 시작 {#initiate-authorization}

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

인증 응답을 가져옵니다. 

| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authorization | 스트리밍 앱</br></br>또는</br></br>프로그래머 서비스 | 1. 요청자(필수)</br>2.  deviceId(필수)</br>3.  자원(필수)</br>4.  device_info/X-Device-Info(필수)</br>5.  _deviceType_</br> 6.  _deviceUser_ (더 이상 사용되지 않음)</br>7.  _appId_ (더 이상 사용되지 않음)</br>8.  추가 매개 변수(선택 사항) | GET | 실패한 경우 인증 세부 사항 또는 오류 세부 정보가 포함된 XML 또는 JSON입니다. 아래 샘플을 참조하십시오. | 200 - 성공  </br>403 - 성공 없음 |

{style=&quot;table-layout:auto&quot;}

</br>


| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| 리소스 | resourceId(또는 MRSS 조각)를 포함하는 문자열로서, 사용자가 요청한 컨텐츠를 식별하고 MVPD 인증 끝점에 의해 인식됩니다. |
| device_info/</br></br>X-Device-Info | 스트리밍 장치 정보.</br></br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br></br>자세한 내용은 [장치 및 연결 정보 전달](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br></br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다. |
| _appId_ | 애플리케이션 ID/이름입니다. </br></br>**참고**: device_info는 이 매개 변수를 대체합니다. |
| 추가 매개 변수 | 호출에는 다음과 같은 다른 기능을 활성화하는 선택적 매개 변수가 포함될 수도 있습니다.</br></br>* generic_data - [프로모션 TempPass](https://tve.helpdocsonline.com/promotional-temp-pass)</br></br>예: `generic_data=("email":"email@domain.com")` |

{style=&quot;table-layout:auto&quot;}

>[!CAUTION]
>
>**스트리밍 장치 IP 주소**</br>
>클라이언트-서버 구현의 경우 스트리밍 장치 IP 주소가 이 호출을 사용하여 암시적으로 전송됩니다.  서버 간 구현의 경우, 여기서 **regcode** 는 스트리밍 장치가 아니라 Programmer Service에 의해 수행되며 스트리밍 장치 IP 주소를 전달하려면 다음 헤더가 필요합니다.</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>여기서 `<streaming\_device\_ip>` 는 스트리밍 장치 공개 IP 주소입니다.</br></br>
>예 :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### 샘플 응답 {#sample-response}

* **사례 1: 성공**

</br>
  **XML:**
  </br>
    "XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
    <expires>1348148289000</expires>
    <mvpd>sampleMvpdId</mvpd>
    <requestor>sampleRequestorId</requestor>
    <resource>sampleResourceId</resource>
    </authorization>
    "



* **JSON:**

   ```JSON
   {
     "mvpd": "sampleMvpdId",
     "resource": "sampleResourceId",
     "requestor": "sampleRequestorId",
     "expires": "1348148289000"
   }
   ```

>[!IMPORTANT]
>
>프록시 MVPD에서 응답이 오면 이름이 지정된 추가 요소가 포함될 수 있습니다 `proxyMvpd`. 

 

* **사례 2: 승인 거부**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```

[REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
