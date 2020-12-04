---
description: AdobeTVSDKConfig.json에서는 기본 규칙과 특정 영역에 대한 규칙을 지정할 수 있습니다.
seo-description: AdobeTVSDKConfig.json에서는 기본 규칙과 특정 영역에 대한 규칙을 지정할 수 있습니다.
seo-title: 크리에이티브 선택 규칙 샘플
title: 크리에이티브 선택 규칙 샘플
uuid: 58e6637e-9f5c-471a-8bc8-d217b36e5f9d
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 디자인 선택 규칙 샘플 {#sample-creative-selection-rules}

AdobeTVSDKConfig.json에서는 기본 규칙과 특정 영역에 대한 규칙을 지정할 수 있습니다.

## 샘플 기본 규칙 {#section_xy4_3fx_hz}

다음은 기본 규칙만 정의하는 [!DNL AdobeTVSDKConfig.json] 파일의 예입니다.

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "type": "priority",
                    "stream": "vod",
                    "priority": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    "type": "priority",
                    "stream": "live",
                    "priority": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    "type": "normalize",
                    "item": "host",
                    "matches": "ew",
                    "values": [
                        "redirector.gvt1.com"
                    ],
                    "find": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "replace": "videoplayback/$1/expire//$2/signature//"
                }
            ]
        }
    }
}
```

## 추가 영역 규칙 {#section_ocv_3fx_hz}이 있는 기본 규칙 샘플

다음은 기본 규칙을 정의하는 [!DNL AdobeTVSDKConfig.json] 파일과 특정 영역 ID에 대한 추가 규칙의 예입니다(이 경우 **&quot;1234&quot;** 영역).

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "type": "priority",
                    "stream": "vod",
                    "priority": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    "type": "priority",
                    "stream": "live",
                    "priority": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    "type": "normalize",
                    "item": "host",
                    "matches": "ew",
                    "values": [
                        "redirector.gvt1.com"
                    ],
                    "find": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "replace": "videoplayback/$1/expire//$2/signature//"
                }
            ],
            
<b>"1234"</b>: [
                {
                    "type": "priority",
                    "matches": "nc",
                    "item": "host",
                    "values": [
                        "my.domain.com",
                        "a.bcd.com"
                    ],
                    "priority": [
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/x-flv",
                        "video/quicktime",
                        "video/webm",
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/javascript"
                    ]
                }
            ]
        }
    }
}
```

