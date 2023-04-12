---
title: 보호된 리소스 식별
description: 보호된 리소스 식별
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# 보호된 리소스 식별 {#identifying-protected-resources}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 개요 {#overview}

각 권한 부여 요청(또는 권한 확인을 위한 요청)에는 사용자가 액세스를 요청하는 보호된 리소스에 대한 고유 식별자가 포함되어야 합니다. 보호된 리소스는 MVPD와 참여 프로그래머 간에 합의된 대로 모든 수준의 승인된 컨텐츠일 수 있습니다. 잠재적인 보호 리소스는 점점 더 구체적인 세부 기간을 갖는 이 트리 구조에 적합해야 합니다.

- 네트워크
   - 채널
      - 표시
         - 에피소드
            - 자산\
                

</br>

## 미디어 RSS 형식 {#media_rss}

리소스는 간단한 문자열(채널에 대한 고유 식별자)로 식별되거나 Adobe(또는 Adobe Primetime 인증 인증 파트너)와 참여 MVPD 및 프로그래머 간에 합의된 대로 MRSS(Media RSS 형식)로 표시될 수 있습니다. 리소스 지정자로 사용되는 RSS 문자열에는 등급 및 자녀 보호 메타데이터와 같은 추가 정보가 포함될 수 있습니다.\
 

&quot;TNT&quot;와 같은 단순 리소스 식별자를 사용하는 경우 채널을 나타내는 것으로 가정되고 이 RSS 리소스 지정자로 변환됩니다.

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

더 복잡한 지정자에는 추가 등급 정보와 같은 정보가 포함될 수 있습니다. 리소스 ID가 필요한 Access Enabler 함수에 전체 RSS 문자열을 전달할 수 있습니다. [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

리소스 지정자는 Adobe Primetime 인증에 불투명합니다. 그것들은 단순히 MVPD에게 전달된다. MVPD가 리소스 지정자를 인식하지 못하거나 구문 분석할 수 없는 경우 오류를 Adobe Primetime 인증으로 반환하여 오류를 사용자에게 다시 전달합니다 `tokenRequestFailed()` 콜백입니다.

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->