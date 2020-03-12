---
description: Primetime 참조 구현에서는 응답에 JSON 기반 피드 형식을 사용합니다. 이 형식은 IFeedItemAdapter 인터페이스의 구현을 사용하여 구문 분석됩니다.
seo-description: Primetime 참조 구현에서는 응답에 JSON 기반 피드 형식을 사용합니다. 이 형식은 IFeedItemAdapter 인터페이스의 구현을 사용하여 구문 분석됩니다.
seo-title: 카탈로그 형식
title: 카탈로그 형식
uuid: 6e1a526f-c0bb-403d-a792-666caf5479a5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 카탈로그 형식 {#catalog-format}

Primetime 참조 구현에서는 응답에 JSON 기반 피드 형식을 사용합니다. 이 형식은 IFeedItemAdapter 인터페이스의 구현을 사용하여 구문 분석됩니다.

>[!NOTE]
>
>이 피드 형식은 참조 구현에서 사용하는 샘플 포맷으로, 형식을 파싱하고 피드 인터페이스에 매핑할 수 있는 방법의 예입니다. 자체 피드 인터페이스 구현에서 고유한 입력 피드 형식을 사용할 수 있습니다.

높은 수준의 형식은 일련의 콘텐트 항목으로 구성됩니다. 각 항목은 게시된 실시간 또는 VOD 비디오 컨텐츠를 나타냅니다.

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
| `id` | 피드 게시 시스템에서 설정한 컨텐츠에 대한 고유 식별자/안내서입니다. |
| `title` | 컨텐츠의 제목입니다. |
| `description` | 컨텐트에 대한 설명입니다. |
| `categories` | 애플리케이션의 사용자 경험을 개선하기 위해 사용할 수 있는 컨텐츠에 대해 태그로 지정된 카테고리 목록입니다. 컨텐츠의 속성을 읽어보십시오. |
| `keywords` | 애플리케이션에서 쉼표로 구분된 키워드 목록을 사용하여 사용자 경험을 향상시킬 수 있습니다. 컨텐츠의 속성을 읽어보십시오. |
| `isLive` | 실시간 또는 VOD 스트림인지 나타내는 true 또는 false |
| `content` | 해당 URL과 함께 컨텐츠에 대한 대체 형식이 있는 JSON 개체의 배열입니다. 예를 들어 f4m 및 m3u8 포맷에 대한 URL이 있을 수 있습니다. JSON 개체 속성은 아래에 자세히 설명되어 있습니다. |
| `thumbnails` | 다양한 크기의 축소판을 위한 URL이 있는 JSON 개체의 배열입니다. JSON 개체 속성은 아래에 정의되어 있습니다. |
| `metadata` | 컨텐츠에 대한 메타데이터를 정의하는 JSON 개체로서 현재 이 메타데이터는 광고 관련 메타데이터로 제한됩니다. 메타데이터 개체는 아래에 정의되어 있습니다. |

다음 코드 블록은 **컨텐츠 개체의**&#x200B;배열을 구성하는 JSON 개체를 정의합니다.

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
| format | Android의 경우 m3u8 형식이어야 합니다. |
| url | 지정된 형식의 비디오 스트림에 대한 URL입니다. |

다음 코드 블록은 **축소판 개체의**&#x200B;배열을 구성하는 JSON 개체를 정의합니다.

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
| format | 축소판 파일의 형식(예: JPEG, PNG)을 나타내는 문자열 |
| 높이 | 축소판의 높이입니다. 참조 응용 프로그램에서, 높이와 너비가 가장 작은 축소판은 작은 축소판으로 반환되고 너비와 높이가 가장 큰 축소판은 큰 축소판으로 반환됩니다. |
| 너비 | 축소판의 폭입니다. 참조 응용 프로그램에서, 높이와 너비가 가장 작은 축소판은 작은 축소판으로 반환되고 너비와 높이가 가장 큰 축소판은 큰 축소판으로 반환됩니다. |
| url | 축소판 파일의 URL입니다. |

다음 코드 블록은 **메타데이터 개체를**&#x200B;정의합니다.

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
| ad | 광고 관련 메타데이터 |
| type | Primetime 광고, 직접 광고 중단 또는 맞춤형 광고 마커가 가치 창출 <br/><br/>PSDK 파섹Adobe Primetime 광고 서비스(Primetime 광고)를 위한 Auditude 관련 메타데이터, 광고 URL을 사용한 직접 광고 중단(직접 광고 중단), 각 광고 마커의 시간 범위를 제공하는 사용자 정의 광고 마커(사용자 정의 광고 마커). 각 유형에는 메타데이터를 처리하는 PSDK에 내장된 AdProvider가 있습니다.  <br/><br/>각 JSON 형식은 아래에 정의되어 있습니다. |
| 세부 정보 | 광고 메타데이터 속성을 포함합니다. 두 광고 메타데이터 유형에는 아래에 정의된 고유한 속성 세트가 있습니다. 내장 유형의 경우, 포함된 속성은 해당 유형에 대해 PSDK에서 예상하는 데이터를 정의합니다. |
| 권한 부여 | 권한 부여 관련 메타데이터 |
| id | Adobe Primetime 유료 TV 전달 서비스에 대한 인증 요청에 사용되는 미디어 리소스 ID입니다. ID는 텍스트 문자열 또는 HTML 인코딩 mRSS 문자열일 수 있습니다. 인증이 필요한 모든 미디어 컨텐츠에는 유효한 리소스 ID가 있어야 합니다. |

