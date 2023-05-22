---
title: 권한 부여 리소스 ID에 대한 JSON 개체
description: 다음 코드 블록은 자격 리소스 ID가 단순 텍스트 문자열인 경우 JSON 개체의 예를 제공합니다.
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 권한 부여 리소스 ID에 대한 JSON 개체 {#json-object-for-entitlement-resource-id}

다음 코드 블록은 자격 리소스 ID가 단순 텍스트 문자열인 경우 JSON 개체의 예를 제공합니다. 이 경우 리소스 ID는 문자열 &quot;resource&quot;입니다.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

다음 코드 블록은 자격 리소스 ID가 HTML으로 인코딩된 mRSS 문자열인 경우 JSON 개체의 예를 제공합니다.

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

다음 mRSS 문자열이 리소스 ID로 사용됩니다.

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
