---
description: Bento4 packager와 Adobe 오프라인 packager를 모두 사용하여 암호화된 DASH 콘텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.
title: Bento4로 콘텐츠를 패키징합니다.
exl-id: c873eaf6-c738-4f95-a900-a8aecb03754d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Widevine 및 PlayReady 패키지 콘텐츠 {#package-for-widevine}

Bento4 packager와 Adobe 오프라인 packager를 모두 사용하여 암호화된 DASH 콘텐츠를 작성합니다. Bento4는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.

## Bento4로 콘텐츠를 패키징합니다.{#package-your-content-with-bento}

Bento4 packager는 입력 mp4가 미리 단편화될 것으로 예상한다. Bento4 packager 배포에는 이를 위한 도구가 포함되어 있습니다.

**Bento4 호출**

일반적인 Bento4 패키지 호출은 아래 예와 같습니다.

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

아래 예제에서는 PlayReady 및 Widevine 체계를 결합합니다. 이 경우 팩커서는 Widevine 콘텐츠 보호 및 PlayReady 콘텐츠 보호 초기화 데이터를 출력 DASH 콘텐츠에 추가합니다.

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

위치

에 대한 값 `--encryption-key` 플래그가 형식입니다. `<base16 encoded key id>:<base16 encoded encryption key>`.

다음 `--widevine-header=provider:intertrust#content_id:2a` 플래그는 현재 TVSDK에서 재생에 필요한 매니페스트에 pssh 상자를 포함하도록 패키지 관리자에 지시합니다.

값 `-playready-header` 은(는) PlayReady 라이센스 획득을 위한 것입니다.

## Adobe Offline Packager로 콘텐츠 패키지 {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.

**Adobe 오프라인 패키지 호출 중**

일반적인 adobe offline packager 호출은 아래 호출과 비슷합니다.

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

이 경우 오프라인 패키저는 Widevine 콘텐츠 보호 및 PlayReady 콘텐츠 보호 초기화 데이터를 출력 DASH 콘텐츠에 추가합니다. 값: `-key_file_path` 는 base64로 인코딩된 키용입니다. 값: `-playready_LA_URL` 은(는) PlayReady 라이센스 획득을 위한 것입니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

특정 Android 장치(주로 Amazon Fire TV)는 오디오 암호 해독을 지원하지 않으므로 오디오 암호화는 선택 사항입니다.
