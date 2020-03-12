---
description: AdobeTVSDKConfig.json에서는 기본 규칙과 특정 영역에 대한 규칙을 지정할 수 있습니다.
seo-description: AdobeTVSDKConfig.json에서는 기본 규칙과 특정 영역에 대한 규칙을 지정할 수 있습니다.
seo-title: 크리에이티브 선택 규칙 샘플
title: 크리에이티브 선택 규칙 샘플
uuid: 7b4b4a76-f813-4f6c-ac41-36ca08bb8173
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 크리에이티브 선택 규칙 샘플{#sample-creative-selection-rules}

에서 `AdobeTVSDKConfig.json` 기본 규칙과 특정 영역에 대한 규칙을 지정할 수 있습니다.

## 샘플 기본 규칙 {#section_xy4_3fx_hz}

다음은 기본 규칙만 정의하는 `AdobeTVSDKConfig.json` 파일의 예입니다.

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

## 추가 영역 규칙이 있는 샘플 기본 규칙 {#section_ocv_3fx_hz}

다음은 기본 규칙을 정의하는 [!DNL AdobeTVSDKConfig.json] 파일과 특정 영역 ID에 대한 추가 규칙(이 경우 영역 **&quot;1234&quot;**)의 예입니다.

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

