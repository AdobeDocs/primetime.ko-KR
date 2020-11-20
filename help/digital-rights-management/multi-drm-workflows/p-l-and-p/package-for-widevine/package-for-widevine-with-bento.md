---
description: Bento4 Packager와 Adobe 오프라인 패키지를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
seo-description: Bento4 Packager와 Adobe 오프라인 패키지를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
seo-title: Bento4로 컨텐츠 패키징
title: Bento4로 컨텐츠 패키징
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: 75702ea2a524d7b38bb9ac83cb094c8482b1098f
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Widevine 및 PlayReady용 컨텐츠 패키징 {#package-for-widevine}

Bento4 Packager와 Adobe 오프라인 패키지를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.

## Bento4로 컨텐츠 패키징{#package-your-content-with-bento}

Bento4 패키저에서는 입력 mp4가 미리 조각화되어 있어야 합니다. Bento4 Packager 배포에는 이를 위한 도구가 포함되어 있습니다.

**Bento4 호출**

일반적인 Bento4 Packager 호출은 아래 예제와 비슷합니다.

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

아래 예에는 PlayReady 및 Widevin 체계가 결합되어 있습니다. 이 경우 Packager는 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다.

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

where

플래그 값이 `--encryption-key` 양식에서 있습니다 `<base16 encoded key id>:<base16 encoded encryption key>`.

플래그는 현재 재생에 필요한 TVSDK인 manifest에 pssh 상자를 포함하도록 패키저에게 알립니다. `--widevine-header=provider:intertrust#content_id:2a`

값은 PlayReady 라이센스 `-playready-header` 획득에 대한 것입니다.

## Adobe Offline Packager를 사용하여 컨텐츠 패키징 {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.

**Adobe 오프라인 패키저 호출**

일반적인 adobe 오프라인 패키지 호출은 아래 호출과 비슷합니다.

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

이 경우 오프라인 패키저가 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다. 의 값 `-key_file_path` 은 base64로 인코딩된 키 값입니다. 의 값 `-playready_LA_URL` 은 PlayReady 라이센스 획득을 위한 것입니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

특정 Android 디바이스(주로 Amazon Fire TV)는 오디오 암호 해독을 지원하지 않으므로 오디오 암호화는 선택 사항입니다.
