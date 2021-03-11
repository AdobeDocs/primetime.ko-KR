---
description: Adobe Offline Packager는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.
title: Adobe Offline Packager를 사용하여 콘텐츠 패키징
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}로 콘텐트 패키징

Adobe Offline Packager는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.

**Adobe Offline Packager 호출**

일반적인 adobe 오프라인 패키지 호출은 아래 호출과 비슷합니다.

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d7dc ecf31a8ebf1b7dda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
     
    -playready_keyid c595f214d84d8dc31a8ebf b7ddd7da_contentc5f595f1ebf 14d84dc7ecf31a8ebf1b7dda5

이 경우 오프라인 패키저에서 Widevine 컨텐츠 보호 및 PlayReady 컨텐츠 보호 초기화 데이터를 출력 DASH 컨텐츠에 추가하고 있습니다. `-key_file_path`의 값은 base64 인코딩 키에 해당합니다. `-playready_LA_URL`의 값은 PlayReady 라이센스 획득에 사용됩니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

특정 Android 디바이스(주로 Amazon Fire TV)는 오디오 암호 해독을 지원하지 않으므로 오디오 암호화는 선택 사항입니다.
