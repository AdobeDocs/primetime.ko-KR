---
title: 매니페스트 재작성 및 광고 가져오기 규칙
description: '매니페스트 재작성 및 광고 가져오기 규칙 '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 매니페스트 다시 작성 및 광고 가져오기 규칙 {#manifest-rewriting}

Primetime Ad Insertion은 간단한 검색/바꾸기 규칙을 사용하여 조각을 다시 작성하고 자산을 가져올 수 있습니다.  TLS 핸드셰이크를 제거하여 성능을 향상시켜주는 http 요청으로 https를 다운 변환하는 데 사용할 수 있습니다.  또한 동일한 CDN의 광고 자산 및 cdn 자산을 전달하는 데 사용할 수 있습니다.

규칙은 정규식 검색/바꾸기로 정의되며, 매니페스트에 삽입한 후뿐만 아니라 전송 전에 url을 변형하는 데 사용할 수 있습니다.

이 예제 규칙은 모든 광고 요청을 https에서 http로 다운로드합니다.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

다음 규칙은 컨텐츠 CDN을 사용하여 Adobe의 광고 저장 장치 CDN에 있는 광고를 전달합니다.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

규칙은 실행할 규칙의 쉼표로 구분된 목록인 Bootstrap API에서 `ptprotoswitch` 매개 변수를 수정하여 이름을 지정하고 활성화/비활성화할 수 있습니다.  예를 들어 다음 두 규칙을 모두 `ptprotoswitch=adfetch_rule1,adfetch_rule2`으로 설정하여 실행할 수 있습니다.

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

계정에 대해 이러한 규칙을 만들거나 활성화하려면 기술 지원에 문의하십시오.