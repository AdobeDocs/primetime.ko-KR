---
seo-title: 정책 워크플로우 세부 사항
title: 정책 워크플로우 세부 사항
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---


# BEES 작업 과정 {#bees-workflow}

**요약:**

* **정책**  - 이 정책을 사용하여 패키지된 모든 컨텐츠에 BEES가 필요하다는 것을 나타내는 DRM BEES 인식 정책을 만듭니다.
* **패키징**  - BEES 인식 DRM 정책을 사용하여 컨텐츠를 패키지화할 수 있습니다.
* **인증**  - 클라이언트 디바이스를 인증하고 Primetime DRM API 또는 Primetime API를 사용하여 이 토큰을 Primetime Cloud DRM과 연결합니다. 이렇게 하면 클라이언트 장치가 모든 라이선스 요청과 함께 Primetime Cloud DRM까지 이 인증 토큰을 전송합니다. Primetime Cloud DRM은 이 기술을 처리하지 않지만 대신 처리를 위해 BEES 끝점에 불투명 물방울로 전달합니다.
* **라이선스**  - 보호된 콘텐츠에 대한 라이선스를 요청합니다. 클라이언트 장치가 이전에 설정한 인증 토큰을 호출에 자동으로 추가합니다.
* **자격 부여**  - Primetime Cloud DRM은 컨텐츠가 BEES를 필요로 하는 정책으로 패키지되었다고 판단합니다. Primetime Cloud DRM은 BEES 종단점으로 보내기 위한 JSON 요청을 구성합니다. BEES 담당자는 Primetime Cloud DRM에 라이선스 발급 여부 및 선택적으로 사용할 DRM 정책에 대해 지시합니다.

## 정책 워크플로 세부 정보 {#policy-workflow-details}

Primetime Cloud DRM이 라이선스 요청을 처리하는 경우 콘텐츠를 표시하기 전에 요청에 DRM 정책을 구문 분석하여 백엔드 권한 부여 서비스에 대한 호출이 필요한지 여부를 확인합니다. BEES 호출 *이*&#x200B;이면 Primetime Cloud DRM이 BEES 요청을 만든 다음 DRM 정책을 분석하여 BEES 요청에 대해 지정된 BEES URL 끝점을 가져옵니다.

정책에서 다음 두 개의 사용자 지정 속성을 지정하여 BEES 요구 사항을 나타내는 DRM 정책을 적용합니다.

    * &#39;policy.customProp.1=bees.required=&lt;true>&#39;
    * &#39;policy.customProp.2=bees.url=&lt;url to=&quot;&quot; your=&quot;&quot; BEES=&quot;&quot; endpoint=&quot;&quot;>&#39;

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

예를 들어 Primetime DRM 정책 관리자( [!DNL AdobePolicyManager.jar])를 사용하면 [!DNL flashaccesstools.properties] 구성 파일에 다음 두 개의 사용자 지정 속성을 지정할 수 있습니다.

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>이미 다른 속성에 `policy.customProp.1` 또는 `policy.customProp.2`을(를) 사용하고 있는 경우 새로운 속성에 고유한 숫자를 사용하면 됩니다.

## 패키지 워크플로우 세부 정보 {#package-workflow-details}

Adobe 액세스 보호 콘텐츠를 패키징하는 동안 BEES 인식 DRM 정책 중 하나를 컨텐츠에 적용해야 합니다.

## 인증 워크플로 세부 정보 {#authentication-workflow-details}

BEES 끝점이 권한 부여 결정을 내리기 위해 클라이언트 장치가 인증 정보를 제공해야 합니다. 이를 위해서는 고객별 인증 토큰을 사용하십시오.

Primetime Cloud DRM은 이 토큰을 이해하지 않아도 됩니다. BEES 종단점으로 이 토큰을 전달합니다. 클라이언트 장치는 이 토큰을 만들거나 가져오고 `DRMManager.setAuthenticationToken()` API를 사용하여 이를 설정할 책임이 있습니다.

라이선스 요청과 함께 전송되도록 이 토큰을 Primetime Cloud DRM과 연결하려면 다음을 수행하십시오.

Primetime Cloud DRM용으로 패키지된 콘텐츠의 DRM 메타데이터로 `DRMManager` 개체를 인스턴스화합니다.

`setAuthenticationToken()` 메서드는 지정된 바이트 배열을 `DRMManager` 인스턴스화에 사용된 DRM 메타데이터에 제공된 라이센스 서버 URL과 연결함으로써 작동합니다.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

토큰은 매개 변수로 `.setAuthenticationToken`을 호출하여 토큰이 지워질 때까지 모든 라이선스 요청과 함께 전송됩니다.

## 라이선스 워크플로우 세부 정보{#license-workflow-details}

`mgr.loadVoucher()`으로 전화하여 Primetime Cloud DRM에 라이선스를 요청합니다.

## 권한 부여 요청 및 응답 세부 정보{#entitlement-request-and-response-details}

Primetime Cloud DRM에서 콘텐츠가 BEES 인식 DRM 정책으로 패키지되었다고 판단하면 DRM 정책에 지정된 BEES 끝점으로 전송하기 위해 다음 JSON 요청을 생성합니다.

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

Primetime Cloud DRM은 응답을 사용하여 요청한 장치에 라이선스를 발급해야 하는지 여부와 라이선스 생성 프로세스에 새로운 DRM 정책을 대체해야 하는지 여부를 결정합니다. `isAllowed`이 `true`이고 응답에 정책이 제공되지 않으면 콘텐츠 패키징 시간 동안 사용된 원래 DRM 정책이 라이선스를 생성하는 데 사용됩니다.