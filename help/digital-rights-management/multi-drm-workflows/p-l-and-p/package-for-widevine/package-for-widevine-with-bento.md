---
description: Bento4 Packager와 Adobe 오프라인 패키저를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
seo-description: Bento4 Packager와 Adobe 오프라인 패키저를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
seo-title: Bento4로 컨텐츠 패키징
title: Bento4로 컨텐츠 패키징
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Windows 및 PlayReady용 컨텐츠 패키징 {#package-for-widevine}

Bento4 Packager와 Adobe 오프라인 패키저를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.

## Bento4로 컨텐츠 패키징{#package-your-content-with-bento}

Bento4 패키저에서는 입력 mp4가 사전에 조각화되어 있어야 합니다. Bento4 Packager 배포에는 이를 위한 도구가 포함되어 있습니다.

**Bento4 호출**

일반적인 Bento4 패키지 호출은 아래 예와 같습니다.

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa09fc 0747c7c5ac215b3b
    —widevine
    
    —widevine-header provider:intertrust#content_id:2a &quot;CC_300_640x340x360.mp4&quot;CC_300_60 DASH&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa09fc 0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

아래 예는 PlayReady 및 Widevine 스키마를 결합합니다. 이 경우 Packager는 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다.

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa09fc 0747c7c5ac215b3b
    —playready
    
    
    
    
    
    —playready-header=&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;WidevineIn—widevineEditine—widevine-header=provider:intertrust#id:2a &quot;CC_300_640x360.mp4&quot;를 - &quot;CC_300_640x360_DASH&quot;여기서

플래그 값은 `--encryption-key` 양식에 있습니다 `<base16 encoded key id>:<base16 encoded encryption key>`.

이 `--widevine-header=provider:intertrust#content_id:2a` 플래그는 현재 재생에 필요한 TVSDK인 매니페스트에 pssh 상자를 포함하도록 패키저에게 알립니다.
의 값은 PlayReady 라이선스 `-playready-header` 획득에 사용됩니다.

## Adobe Offline Packager를 사용하여 컨텐츠 패키징 {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.

**Adobe Offline Packager 호출**

일반적인 Adobe 오프라인 패키지 호출은 아래 호출과 비슷합니다.

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7dc ecf31a8ebf1b7dda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    
    -playready_keyid c595f214d84dc7ecf31a8ebf b7ddd_da_idc5f15 14d84dc7ecf31a8ebf1b7dda5

이 경우 오프라인 패키저가 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 파섹 컨텐츠에 추가하고 있습니다. 의 값은 base64 인코딩 키에 `-key_file_path` 사용됩니다. 의 값은 `-playready_LA_URL` PlayReady 라이선스 허용입니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

특정 Android 디바이스 — 기본 Amazon Fire TV — 오디오 암호 해독을 지원하지 않습니다. 오디오 암호화는 선택 사항입니다.