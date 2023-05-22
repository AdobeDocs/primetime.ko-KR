---
title: 매니페스트 재작성 및 광고 가져오기 규칙
description: 매니페스트 재작성 및 광고 가져오기 규칙
exl-id: 3750abc1-da60-4faf-ba85-37914f33641f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 매니페스트 재작성 및 광고 가져오기 규칙 {#manifest-rewriting}

Primetime Ad Insertion은 간단한 검색/바꾸기 규칙을 사용하여 조각을 다시 작성하고 에셋을 가져올 수 있습니다.  이 플러그인을 사용하여 https를 http 요청으로 하향 변환할 수 있으며, 이렇게 하면 TLS 악수를 제거하여 성능이 향상됩니다.  동일한 CDN에서 광고 자산과 cdn 자산을 전달하는 데에도 사용할 수 있습니다.

규칙은 정규 표현식 검색/바꾸기로 정의되며 매니페스트에 삽입한 후뿐만 아니라 보내기 전에 URL을 변환하는 데 사용할 수 있습니다.

이 예제 규칙은 domain.com에 대한 모든 광고 요청을 https에서 http로 다운변환합니다.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

다음 규칙은 컨텐츠 CDN을 사용하여 Adobe의 광고 스토리지 CDN에 있는 광고를 게재합니다.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

규칙 이름을 지정하고 을 수정하여 활성화/비활성화할 수 있습니다. `ptprotoswitch` Bootstrap API의 매개 변수(실행할 규칙의 쉼표로 구분된 목록)입니다.  예를 들어, 이 두 규칙은 모두 을 설정하여 실행할 수 있습니다 `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

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
