---
description: Adobe Offline Packager는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
seo-description: Adobe Offline Packager는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.
seo-title: Adobe Offline Packager를 사용하여 컨텐츠 패키징
title: Adobe Offline Packager를 사용하여 컨텐츠 패키징
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}로 콘텐트 패키징

Adobe Offline Packager는 암호화되지 않은 mp4 컨텐츠를 입력으로 사용합니다.

**Adobe 오프라인 패키저 호출**

일반적인 adobe 오프라인 패키지 호출은 아래 호출과 비슷합니다.

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f218dc7dc ecf31a8ebf1b7dda5
    -widevine_provider intertrust
    -playready_keyid_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
     
    -playready_keyid c595f214d84dc7ecf31a8bf7dda_contentc5f5f11a 14d84dc7ecf31a8ebf1b7dda5

이 경우 오프라인 패키저가 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다. `-key_file_path`의 값은 base64 인코딩 키에 해당합니다. `-playready_LA_URL`의 값은 PlayReady 라이선스 계정에 사용됩니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

특정 Android 디바이스(주로 Amazon Fire TV)는 오디오 암호 해독을 지원하지 않으므로 오디오 암호화는 선택 사항입니다.
