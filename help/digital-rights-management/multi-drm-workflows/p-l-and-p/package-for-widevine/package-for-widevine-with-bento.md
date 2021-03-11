---
description: Bento4 Packager와 Adobe 오프라인 패키지를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
title: Bento4로 컨텐츠 패키징
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Widevine 및 PlayReady용 내용 패키징 {#package-for-widevine}

Bento4 Packager와 Adobe 오프라인 패키지를 모두 사용하여 암호화된 DASH 컨텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.

## Bento4{#package-your-content-with-bento}로 컨텐츠 패키징

Bento4 패키저에서는 입력 mp4가 사전에 조각화되어 있을 것으로 예상하고 있습니다. Bento4 Packager 배포에는 이와 관련된 도구가 포함되어 있습니다.

**벤토4를 호출하는 중**

일반적인 Bento4 Packager 호출은 아래 예와 비슷합니다.

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

아래 예제는 PlayReady 및 Widevin 스킴을 결합합니다. 이 경우 Packager는 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다.

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

`--encryption-key` 플래그의 값은 `<base16 encoded key id>:<base16 encoded encryption key>` 형식입니다.

`--widevine-header=provider:intertrust#content_id:2a` 플래그는 현재 재생에 필요한 TVSDK인 매니페스트에 pssh 상자를 포함하도록 패키저에게 알립니다.

`-playready-header`의 값은 PlayReady 라이센스 획득에 사용됩니다.

## Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}을(를) 사용하여 콘텐트 패키징

Adobe Offline Packager는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.

**Adobe Offline Packager 호출**

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

이 경우 오프라인 패키저에서 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다. `-key_file_path`의 값은 base64 인코딩 키에 해당합니다. `-playready_LA_URL`의 값은 PlayReady 라이센스 획득에 사용됩니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

특정 Android 디바이스(주로 Amazon Fire TV)는 오디오 암호 해독을 지원하지 않으므로 오디오 암호화는 선택 사항입니다.
