---
description: Primetime 참조 구현에서는 응답에 JSON 기반 피드 형식을 사용합니다. 이 형식은 IFeedItemAdapter 인터페이스의 구현을 사용하여 구문 분석됩니다.
title: 카탈로그 형식
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 카탈로그 형식 {#catalog-format}

Primetime 참조 구현에서는 응답에 JSON 기반 피드 형식을 사용합니다. 이 형식은 IFeedItemAdapter 인터페이스의 구현을 사용하여 구문 분석됩니다.

>[!NOTE]
>
>이 피드 형식은 참조 구현에서 사용하는 샘플 형식이며 피드 인터페이스에 형식을 구문 분석하고 매핑할 수 있는 방법의 예로 사용됩니다. 고유한 피드 인터페이스 구현에 고유한 입력 피드 형식을 사용할 수 있습니다.

상위 수준에서 형식은 콘텐츠 항목의 배열로 구성됩니다. 각 항목은 라이브 또는 VOD로 게시된 비디오 컨텐츠를 나타냅니다.

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

각 피드 항목은 지정된 속성 세트가 있는 JSON 개체입니다.

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| 속성 | 설명 |
|---|---|
| `id` | 피드 게시 시스템에서 설정한 컨텐츠에 대한 고유 식별자/안내서. |
| `title` | 콘텐츠 제목. |
| `description` | 콘텐츠에 대한 설명. |
| `categories` | 애플리케이션에서 사용자 경험을 개선하는 데 사용할 수 있는 컨텐츠에 태그된 카테고리 목록입니다. 콘텐츠에 대한 속성을 읽어 보십시오. |
| `keywords` | 애플리케이션에서 사용자 경험을 개선하기 위해 사용할 수 있는 쉼표로 구분된 키워드 목록입니다. 콘텐츠에 대한 속성을 읽어 보십시오. |
| `isLive` | 라이브 또는 VOD 스트림인지 보여 주는 true 또는 false. |
| `content` | 해당 URL과 함께 콘텐츠에 대한 대체 형식이 있는 JSON 개체의 배열입니다. 예를 들어 f4m 및 m3u8 형식에 대한 url이 있을 수 있습니다. JSON 개체 속성은 아래에 자세히 설명되어 있습니다. |
| `thumbnails` | 다양한 크기의 썸네일에 대한 URL이 있는 JSON 개체의 배열입니다. JSON 개체 속성은 아래에 정의되어 있습니다. |
| `metadata` | 콘텐츠에 대한 메타데이터를 정의하는 JSON 개체. 현재 이 메타데이터는 광고 관련 메타데이터로 제한됩니다. 메타데이터 개체가 아래에 정의되어 있습니다. |

다음 코드 블록은 의 배열을 형성하는 JSON 개체를 정의합니다. **콘텐츠 개체**:

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| 속성 | 설명 |
|--- |--- |
| 형식 | Android용 m3u8 형식이어야 합니다. |
| url | 지정된 형식의 비디오 스트림에 대한 URL입니다. |

다음 코드 블록은 의 배열을 형성하는 JSON 개체를 정의합니다. **축소판 개체**:

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| 속성 | 설명 |
|---|---|
| 형식 | 썸네일 파일의 형식을 나타내는 문자열(예: JPEG, PNG 등). |
| 높이 | 썸네일의 높이입니다. 참조 응용 프로그램에서는 가장 작은 높이와 너비의 썸네일이 작은 썸네일로 반환되고 가장 큰 너비와 높이의 썸네일이 큰 썸네일로 반환됩니다. |
| 폭 | 썸네일의 너비입니다. 참조 응용 프로그램에서는 가장 작은 높이와 너비의 썸네일이 작은 썸네일로 반환되고 가장 큰 너비와 높이의 썸네일이 큰 썸네일로 반환됩니다. |
| url | 썸네일 파일의 URL입니다. |

다음 코드 블록은 **메타데이터 개체**:

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| 속성 | 설명 |
|--- |--- |
| 광고 | 광고 관련 메타데이터. |
| 유형 | 값은 Primetime 광고, 직접 광고 브레이크 또는 사용자 지정 광고 마커일 수 있습니다. <br/><br/>PSDK는 Primetime 광고 서비스(Primetime 광고)에 대한 Auditude 관련 메타데이터, 광고 URL이 있는 직접 광고 브레이크(Direct Ad Break) 및 각 광고 마커에 대해 TimeRange를 제공하는 사용자 지정 광고 마커(사용자 지정 광고 마커)와 같은 메타데이터 유형을 기본적으로 지원합니다. 각 유형에는 메타데이터를 처리하는 PSDK에 내장된 AdProvider가 있습니다.  <br/><br/>각 JSON에 대한 JSON 형식은 아래에 정의되어 있습니다. |
| 세부 사항 | 광고 메타데이터 속성을 포함합니다. 두 유형의 광고 메타데이터에는 아래에 정의된 자체 속성 세트가 있습니다. 기본 제공 형식의 경우 포함된 속성은 해당 형식에 대해 PSDK에서 예상하는 데이터를 정의합니다. |
| 권한 부여 | 권한 관련 메타데이터 |
| id | Adobe Primetime pay-TV pass 서비스에 대한 인증 요청에 사용되는 미디어 리소스 ID입니다. 상기 ID는 텍스트 문자열 또는 HTML으로 인코딩된 mRSS 문자열일 수 있다. 인증이 필요한 모든 미디어 콘텐츠에는 유효한 리소스 ID가 있어야 합니다. |
