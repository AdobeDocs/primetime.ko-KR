---
title: Primetime 인증에서 Experience Cloud ID 사용
description: Primetime 인증에서 Experience Cloud ID 사용
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Primetime 인증에서 Experience Cloud ID 사용

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## Experience Cloud ID란 무엇이며 어떻게 얻습니까? {#what-exp-cloud-id-obtain}

Experience Cloud ID(ECID for short)는 애플리케이션/웹 사이트의 각 개별 사용자에 대해 Adobe Experience Cloud에서 생성한 고유 ID입니다. ECID는 여러 애플리케이션/웹 사이트에서 특정 사용자에 대한 정보를 함께 연결하는 데 사용되는 모든 Experience Cloud 보고서에서 주로 사용됩니다.

방문자 ID를 제공하는 시스템이 이미 있는 경우 이 문서의 범위에 대해 동일한 ID를 사용해야 합니다.

ECID를 가져오는 한 가지 방법은 Experience Cloud ID 서비스를 사용하는 것입니다. TDM, JS 라이브러리, 서버 측, 직접 통합 또는 모바일 플랫폼용 기본 라이브러리를 기반으로 하는 기본 구현 유형을 사용할 수 있습니다. 사용 가능한 서비스, 라이브러리, SDK 및 구현 안내서에 대한 포괄적인 보기에 대해서는 다음을 참조하십시오. https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## Primetime 인증에서 Experience Cloud ID를 사용하면 어떤 이점이 있습니까? {#benefit-ex-cloud-id}

ECID를 사용하도록 SDK 및 Clientless REST API를 구성하는 경우 나중에 Primetime 인증에서 수집한 데이터를 기존 Experience Cloud 솔루션에 연결할 수 있습니다. 이를 통해 Adobe에서 제공하는 모든 솔루션에서 고객 여정 및 경험을 더 잘 이해할 수 있습니다.

## Primetime 인증에서 Experience Cloud ID를 사용하는 방법 {#how-to-ex-cloud-id-authn}

ECID(위에 설명됨)를 얻으면 SDK 및 Clientless REST API에 이 정보를 전달해야 합니다. 이 정보는 나중에 SDK에서 수행하는 각 네트워크 호출에서 서버에 전달됩니다. 구성 프로세스는 다음과 같이 모든 SDK에 대해 다릅니다.

### JS SDK {#js-sdk}

JavaScript의 경우 ECID를 맵에 세 번째 매개 변수로 setRequestor 호출에 전달해야 합니다.

**사용 예:**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### iOS/tvOS SDK {#ios-sdk}

iOS/tvOS SDK의 경우 setOptions라는 전용 메서드가 있습니다.

**사용 예:**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### Android/fireTV SDK {#android-sdk}

Android/fireTV SDK의 경우 메커니즘은 iOS과 유사합니다. 매개 변수 이름만 다릅니다. API는 여기에 설명되어 있습니다.

**사용 예:**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### Clientless API {#clientless-api}

REST API를 통해 Adobe Primetime을 사용하는 경우 **ECID** 값을 보내야 합니다. **모든 API에서** 라는 매개 변수로 **&#39;ap_vi&#39;**.

**사용 예:**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`