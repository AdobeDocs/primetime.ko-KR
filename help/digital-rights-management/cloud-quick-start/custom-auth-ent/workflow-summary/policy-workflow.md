---
title: 정책 워크플로우 세부 사항
description: 정책 워크플로우 세부 사항
copied-description: true
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# 벌 작업 과정 {#bees-workflow}

**요약:**

* **정책** - 이 정책을 사용하여 패키지된 모든 콘텐츠에 BEE가 필요함을 나타내는 DRM BEE 인식 정책을 만듭니다.
* **포장** - BEE 인식 DRM 정책을 사용하여 컨텐츠를 패키지화합니다.
* **인증** - 클라이언트 장치를 인증하고 Primetime DRM API 또는 Primetime API를 사용하여 이 토큰을 Primetime Cloud DRM과 연결합니다. 이렇게 하면 클라이언트 장치가 모든 라이선스 요청과 함께 이 인증 토큰을 Primetime Cloud DRM으로 보냅니다. Primetime Cloud DRM은 이 토큰을 처리하지 않지만, 대신 처리를 위해 이 토큰을 BEES 엔드포인트에(불투명 블롭)로 전달합니다.
* **라이선스** - 보호된 콘텐츠에 대한 라이선스를 요청합니다. 클라이언트 장치가 이전에 설정한 인증 토큰을 호출에 자동으로 추가합니다.
* **자격 부여** - Primetime Cloud DRM은 BEE가 필요한 정책과 함께 컨텐츠가 패키지되었음을 결정합니다. Primetime Cloud DRM이 BEES 엔드포인트로 전송하기 위한 JSON 요청을 구성합니다. BEES 응답으로 Primetime Cloud DRM에 라이센스를 발급할지 여부 및 선택적으로 사용할 DRM 정책을 지시합니다.

## 정책 워크플로우 세부 사항 {#policy-workflow-details}

Primetime Cloud DRM이 라이선스 요청을 처리할 때 콘텐츠를 표시하기 전에 백 엔드 자격 서비스에 대한 호출이 필요한지 여부를 확인하기 위해 요청에서 DRM 정책을 구문 분석합니다. BEES가 *is* 필수 Primetime Cloud DRM은 BEES 요청을 만든 다음 DRM 정책을 구문 분석하여 BEE 요청에 대해 지정된 BEE URL 끝점을 가져옵니다.

정책에 다음 두 사용자 지정 속성을 지정하여 BEE 요구 사항을 나타내는 DRM 정책을 적용합니다.

* `policy.customProp.1=bees.required=<true | false>`
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

예를 들어 Primetime DRM 정책 관리자( [!DNL AdobePolicyManager.jar])를 채울 수도 있고, [!DNL flashaccesstools.properties] 구성 파일:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>이미 사용 중인 경우 `policy.customProp.1` 또는 `policy.customProp.2` 다른 속성의 경우 최신 속성에 대해 고유한 숫자를 사용하면 됩니다.

## 패키지 워크플로우 세부 사항 {#package-workflow-details}

Adobe 액세스 보호 콘텐츠를 패키징하는 동안 콘텐츠에 BEE 인식 DRM 정책 중 하나를 적용해야 합니다.

## 인증 워크플로우 세부 사항 {#authentication-workflow-details}

BEES 종단점이 자격 결정을 내리려면 클라이언트 장치가 인증 정보를 제공해야 합니다. 고유한 고객별 인증 토큰을 사용하여 이 작업을 수행합니다.

Primetime Cloud DRM은 이 토큰을 이해할 필요가 없습니다. 이 토큰을 BEES 종단점으로 전달하면 됩니다. 클라이언트 장치는 이 토큰을 만들거나 가져오고 이 토큰을 사용하여 설정해야 합니다 `DRMManager.setAuthenticationToken()` API.

라이선스 요청과 함께 전송되도록 이 토큰을 Primetime Cloud DRM 과 연결하려면 다음을 수행하십시오.

를 인스턴스화합니다. `DRMManager` primetime Cloud DRM용으로 패키지된 컨텐츠의 DRM 메타데이터를 사용하는 객체입니다.

다음 `setAuthenticationToken()` 메서드는 지정된 바이트 배열을 인스턴스화하는 데 사용된 DRM 메타데이터에 제공된 라이선스 서버 URL과 연결하여 작동합니다 `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

토큰은 를 호출하여 토큰이 지워질 때까지 모든 라이선스 요청으로 전송됩니다 `.setAuthenticationToken` 매개 변수로 null 사용.

## 라이선스 워크플로우 세부 정보{#license-workflow-details}

를 호출하여 Primetime Cloud DRM에서 라이선스 요청 `mgr.loadVoucher()`.

## 권한 부여 요청 및 응답 세부 정보{#entitlement-request-and-response-details}

Primetime Cloud DRM에서 컨텐츠가 BEE 인식 DRM 정책과 함께 패키지화되었다고 판단되면 DRM 정책에 지정된 BEES 종단점으로 전송하기 위한 다음 JSON 요청을 구성합니다.

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

BEES 끝점에서 다음 응답이 필요합니다.

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

Primetime Cloud DRM은 응답을 사용하여 요청 장치에 라이선스를 발급해야 하는지, 라이선스 생성 프로세스에 새 DRM 정책을 대체해야 하는지 여부를 결정합니다. If `isAllowed` is `true` 응답에 정책이 제공되지 않으면 콘텐츠 패키징 시간 동안 사용된 원래 DRM 정책이 라이선스를 생성하는 데 사용됩니다.
