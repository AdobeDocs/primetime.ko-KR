---
description: 권한 부여 요청 및 응답은 라이선스 서버와 고객의 권한 부여 서비스 간에 상호 인증된 SSL 연결을 통해 전달됩니다.
title: 공개 API 보기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# 공개 API {#sees-public-api} 표시

권한 부여 요청 및 응답은 라이선스 서버와 고객의 권한 부여 서비스 간에 상호 인증된 SSL 연결을 통해 전달됩니다.

HTTPS URI 스키마( [https://tools.ietf.org/html/rfc7230#section-2.7.2](https://tools.ietf.org/html/rfc7230#section-2.7.2))는 권한 부여 끝점을 정의하는 데 사용되며 HTTP POST 요청 메서드( [https://tools.ietf.org/html/rfc7231#section-4.3.3](https://tools.ietf.org/html/rfc7231#section-4.3.3))는 요청에 사용됩니다. 백엔드 자격 부여를 나타내는 플래그와 권한 부여 끝점은 필수 사항이며 패키징 시 정책에 포함되어야 합니다.

## 권한 부여 요청 {#section_BFBFEF0795CA46D6842C479256B95F95}

권한 부여 요청의 본문은 아래와 같이 정의된 JSON 개체입니다.

**JSON 권한 부여 요청 개체 정의**

```
{ 
 "title" : "Entitlement Request", 
 "type" : "object", 
 "properties" : { 
  "messageID" : { 
   "type" : "string", 
   "description" : "Unique ID for this message (GUID).  Used to confirm that the subsequent response is actually for this request." 
  }, 
  "version" : { 
   "type" : "integer", 
   "description" : "Version number of the protocol, currently 1." 
  }, 
  "requestType" : { 
   "type" : "integer", 
   "description" : "Request type. 1 - time based entitlement request, 2 - device registration entitlement request 3 - device bound entitlement request." 
  }, 
  "contentID" : { 
   "type" : "string", 
   "description" : "Content ID (GUID) that was given to the content during packaging time." 
  }, 
  "customerCookie" : { 
   "type" : "string", 
   "description" : "Customer cookie. Cookie is just arbitrary string up to 32 characters long." 
  } 
    }, 
 "required" : ["messageID", "version", "contentID"] 
}
```

## 권한 부여 응답 {#section_F15A9FD6BAD946B3B4C5C14612F90154}

권한 부여 응답의 본문은 JSON 개체입니다.

**JSON 권한 응답 개체 정의**

```
{ 
  "title" : "Entitlement Response", 
  "type" : "object", 
  "properties" : { 
    "messageID" : { 
    "type" : "string", 
    "description" : "Unique ID from the Entitlement Request message.   
      Must match, or entitlement will be denied." 
  }, 
  "version" : { 
    "type" : "integer", 
    "description" : "Version number of the protocol; must be <= the version number  
      from the Entitlement Request message." 
  }, 
  "isAllowed" : { 
    "type" : "boolean", 
    "description" : "Grant the license or not." 
  }, 
  "epTokenURL" : { 
    "type" : "string", 
    "description" : "ExpressPlay Token URL" 
  }, 
  "error" : { 
    "type" : "integer", 
    "description" : "An error number produced by the entitlement server.  
      Will be passed to the client as the 'code' field of the server error response." 
  }, 
  "errorText" : { 
    "type" : "string", 
    "description" : "Additional error information produced by the entitlement server.  
      Will be passed to the client as the 'text' field of the server error response." 
  }, 
  "required" : ["messageID", "version", "isAllowed", "epTokenURL"] 
}
```
