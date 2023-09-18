---
description: Adobe Offline Packager는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.
title: Adobe Offline Packager로 콘텐츠 패키지
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Adobe Offline Packager로 콘텐츠 패키지{#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager는 암호화되지 않은 mp4 콘텐츠를 입력으로 사용합니다.

**Adobe 오프라인 패키지 호출 중**

일반적인 adobe offline packager 호출은 아래 호출과 비슷합니다.

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -widevine_provider 상호 트러스트
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7dda5

이 경우 오프라인 패키저는 Widevine 콘텐츠 보호 및 PlayReady 콘텐츠 보호 초기화 데이터를 출력 DASH 콘텐츠에 추가합니다. 값: `-key_file_path` 는 base64로 인코딩된 키용입니다. 값: `-playready_LA_URL` 은(는) PlayReady 라이센스 획득을 위한 것입니다.

conf_path 인수는 다음을 포함하는 구성 파일을 가리킵니다.

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

특정 Android 장치(주로 Amazon Fire TV)는 오디오 암호 해독을 지원하지 않으므로 오디오 암호화는 선택 사항입니다.
