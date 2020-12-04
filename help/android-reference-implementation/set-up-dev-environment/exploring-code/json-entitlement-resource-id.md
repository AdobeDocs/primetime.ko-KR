---
seo-title: 권한 부여 리소스 ID용 JSON 개체
title: 권한 부여 리소스 ID용 JSON 개체
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: 권한 부여 리소스 ID가 간단한 텍스트 문자열인 경우 다음 코드 블록은 JSON 개체의 예를 제공합니다.
seo-description: 권한 부여 리소스 ID가 간단한 텍스트 문자열인 경우 다음 코드 블록은 JSON 개체의 예를 제공합니다.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 권한 부여 리소스 ID {#json-object-for-entitlement-resource-id}에 대한 JSON 개체

권한 부여 리소스 ID가 간단한 텍스트 문자열인 경우 다음 코드 블록은 JSON 개체의 예를 제공합니다. 이 경우 리소스 ID는 문자열 &quot;resource&quot;입니다.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

권한 부여 리소스 ID가 HTML 인코딩 mRSS 문자열인 경우 다음 코드 블록은 JSON 개체의 예를 제공합니다.

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
