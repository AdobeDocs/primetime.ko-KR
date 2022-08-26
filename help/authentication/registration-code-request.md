---
title: 등록 페이지
description: 등록 페이지
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# 등록 페이지 {#registration-page}

## REST API 엔드포인트 {#clientless-endpoints}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

&lt;reggie_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 프로덕션 - [api.auth.adobe.com](http://api.auth.adobe.com/)
* 스테이징 - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## 설명 {#create-reg-code-svc}

임의로 생성된 등록 코드 및 로그인 페이지 URI를 반환합니다.

| 끝점 | 호출됨  </br>기준 | 입력   </br>매개 변수 | HTTP  </br>메서드 | 응답 | HTTP  </br>응답 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/register/v1/{requestor}/regcode</br>예:</br>REGIE_FQDN/regie/v1/sampleRequestorId/regcode | 스트리밍 앱</br>또는</br>프로그래머 서비스 | 1. 요청자  </br>    (경로 구성 요소)</br>2.  deviceId(해시됨)   </br>    (필수입니다)</br>3.  device_info/X-Device-Info(필수)</br>4.  mvpd(선택 사항)</br>5.  ttl(선택 사항)</br>6.  _deviceType_</br> 7.  _deviceUser_ (더 이상 사용되지 않음)</br>8.  _appId_ (더 이상 사용되지 않음) | POST | 실패한 경우 등록 코드 및 정보 또는 오류 세부 정보가 포함된 XML 또는 JSON입니다. 아래의 스키마 및 샘플을 참조하십시오. | 201년 |

{style=&quot;table-layout:auto&quot;}

| 입력 매개 변수 | 설명 |
| --- | --- |
| 요청자 | 이 작업이 유효한 ProgrammerId입니다. |
| deviceId | 장치 ID 바이트입니다. |
| device_info/</br>X-Device-Info | 스트리밍 장치 정보.</br>**참고**: 이 URL은 URL 매개 변수로서 device_info를 전달할 수 있지만 이 매개 변수의 잠재적 크기와 GET URL의 길이에 대한 제한 사항으로 인해 http 헤더에서 X-Device-Info로 전달해야 합니다. </br>자세한 내용은 [장치 및 연결 정보 전달](http://tve.helpdocsonline.com/passing-device-information). |
| mvpd | 이 작업이 유효한 MVPD ID입니다. |
| ttl | 이 레지코드는 몇 초 후에 작동해야 합니다.</br>**참고**: ttl에 허용되는 최대 값은 36000초(10시간)입니다. 값이 높으면 400 HTTP 응답(잘못된 요청)이 발생합니다. If `ttl` 가 비어 있으면 Primetime 인증은 기본값 30분을 설정합니다. |
| _deviceType_ | 장치 유형(예: Roku, PC)입니다.</br>이 매개 변수가 올바르게 설정되면 ESM은 다음 지표를 제공합니다 [장치 유형별 분류](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) clientless를 사용하는 경우 Roku, AppleTV, Xbox 등과 같은 다양한 유형의 분석을 수행할 수 있습니다.</br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**참고**: device_info가 이 매개 변수를 대체합니다. |
| _deviceUser_ | 장치 사용자 식별자입니다. |
| _appId_ | 애플리케이션 ID/이름입니다. </br>**참고**: device_info는 이 매개 변수를 대체합니다. |

{style=&quot;table-layout:auto&quot;}


>[!CAUTION]
>
>**스트리밍 장치 IP 주소**
></br>
>클라이언트-서버 구현의 경우 스트리밍 장치 IP 주소가 이 호출을 사용하여 암시적으로 전송됩니다.  서버 간 구현의 경우, 여기서 **regcode** 는 스트리밍 장치가 아닌 Programmer Service로 설정되며, 스트리밍 장치 IP 주소를 전달하려면 다음 헤더가 필요합니다.
>
>
>
```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>여기서 `<streaming\_device\_ip>` 는 스트리밍 장치 공개 IP 주소입니다.
></br></br>
>예 :</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1</br>X-Forwarded-For:203.45.101.20
>```
</br>

### 응답 XML 스키마 {#xml-schema}


#### 등록 코드 XSD {#registration-code-xsd}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>
```

 </br>

| 요소 이름 | 설명 |
| --------------- | ------------------------------------------------------------------------------------ |
| id | 등록 코드 서비스에서 생성한 UUID |
| 코드 | 등록 코드 서비스에서 생성한 등록 코드 |
| 요청자 | 요청자 ID |
| mvpd | Mvpd ID |
| 생성 | 등록 코드 생성 타임스탬프(1970년 1월 1일 GMT 이후 밀리초) |
| 만료 | 등록 코드가 만료되는 타임스탬프(1970년 1월 1일 GMT 이후 밀리초) |
| deviceId | 고유 장치 ID(또는 XSTS 토큰) |
| deviceType | 장치 유형 |
| deviceUser | 사용자가 장치에 로그인함 |
| appId | 애플리케이션 Id |
| appVersion | 애플리케이션 버전 |
| registrationURL | 최종 사용자에게 표시할 로그인 웹 앱의 URL |

{style=&quot;table-layout:auto&quot;}
 </br>

 

### 오류 메시지 XSD  {#error-message}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="rest.pass.adobe.com"
               targetNamespace="rest.pass.adobe.com"
               attributeFormDefault="unqualified"
               elementFormDefault="unqualified">
        <xs:element name="error">
            <xs:complexType>
                <xs:all>
                    <xs:element name="status" type="xs:int" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="message" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="details" type="xs:string" minOccurs="0" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
    </xs:schema>
```
 

### 샘플 응답 {#sample-response}

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```
 
**JSON:**

```JSON
    {
        "id": "678f9fea-9d364b29-246c-488f-b97e-298566d1b9e0",
        "code": "D4BDU2W",
        "requestor": "sampleRequestorId",
        "mvpd": "sampleMvpdId",
        "generated": 1348039555877,
        "expires": 1348043155877,
        "info": {
            "deviceId": "dGhpc0l.kQUR1bW15RGV2.aWNlSWQ=",
            "deviceType": "xboxOne",
            "deviceUser": "JD",
            "appId": "2345",
            "appVersion": "2.0",
            "registrationURL": "http://loginwebapp.com"
        }
    }
```

[REST API 참조로 돌아가기](http://tve.helpdocsonline.com/rest-api-reference)
