---
description: 컨텐츠 패키징은 웹을 통해 재생할 비디오 컨텐츠를 준비하는 과정입니다. 패키징에는 Raw 비디오를 매니페스트 파일로 변환하거나 다양한 디바이스 및 브라우저에 맞는 다양한 DRM 솔루션을 사용하여 컨텐츠를 암호화하는 작업이 포함됩니다.
seo-description: 컨텐츠 패키징은 웹을 통해 재생할 비디오 컨텐츠를 준비하는 과정입니다. 패키징에는 Raw 비디오를 매니페스트 파일로 변환하거나 다양한 디바이스 및 브라우저에 맞는 다양한 DRM 솔루션을 사용하여 컨텐츠를 암호화하는 작업이 포함됩니다.
seo-title: 콘텐츠 패키지
title: 콘텐츠 패키지
uuid: b9bc6104-a1ea-4ea0-a0a4-af8a606e5d47
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 콘텐츠 패키지 {#package-your-content}

컨텐츠 패키징은 웹을 통해 재생할 비디오 컨텐츠를 준비하는 과정입니다. 패키징에는 Raw 비디오를 매니페스트 파일로 변환하거나 다양한 디바이스 및 브라우저에 맞는 다양한 DRM 솔루션을 사용하여 컨텐츠를 암호화하는 작업이 포함됩니다.

컨텐츠를 준비하려면 Adobe Offline Packager나 ExpressPlay의 Bento4 Packager와 같은 다른 도구를 사용할 수 있습니다. 패키지 모두 재생을 위해 비디오를 준비하고(예: 원본 파일을 조각 내어 매니페스트에 넣기) 선택한 DRM 솔루션(PlayReady, Widevine, FairPlay, Access 등)을 사용하여 비디오를 보호합니다.:

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay 패키지](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 설치 프로그램을 테스트하는 데 사용할 컨텐츠를 패키지하거나 다른 방법으로 얻을 수 있습니다.

   패키징에 대해 기억해야 할 중요한 포인트 중 하나는 이 패키징 단계에서 사용하는 키 ID(콘텐츠 ID)가 후속 라이선스 토큰 요청에서 제공해야 하는 키와 동일하다는 점입니다. 키 ID는 CEK를 식별하는 유일한 항목입니다(CK는 자체 키 관리 데이터베이스에 저장되거나 ExpressPlay의 키 [저장소 서비스를 사용하여 저장될 수 있습니다](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Adobe Access에 익숙한 사용자에게는 서로 다른 솔루션의 작동 방식이 매우 중요합니다. Access에서 라이센스 키는 DRM 메타데이터에 포함되고 보호된 내용과 함께 앞뒤로 전달됩니다. 여기에 설명된 다중 DRM 시스템에서는 실제 라이센스가 전달되지 않지만 키 ID를 통해 안전하게 저장되고 보관됩니다.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

다음은 Windows용 Adobe Offline Packager를 사용하는 패키징 예입니다. Packager는 다음과 같은 구성 파일(예: [!DNL widevine.xml])을 사용합니다.

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path` - 이 항목은 로컬 패키징 시스템에서 소스 비디오 위치를 가리킵니다.
* `out_type` - 이 항목에서는 패키징된 출력의 유형을 설명합니다(이 경우 DASH(HTML5에서 Widevine 보호를 위해).
* `out_path` - 로컬 컴퓨터에서 출력할 위치입니다.
* `drm_sys` - 패키징하는 DRM 솔루션 이것은 `widevine`또는 `fairplay`또는 `playready`입니다.

* `frag_dur` 및 DASH `target_dur` 별 지속 시간 항목은 비디오 재생과 관련이 있습니다.

* `key_file_path` - 패키징 시스템에서 CEK(Content Encryption Key)로 사용되는 라이센스 파일의 위치입니다. Base-64로 인코딩된 16바이트 16진수 문자열입니다.
* `widevine_content_id` - 이것은 위키드빈 &quot;폭탄판&quot; 입니다.항상 그렇습니다 `2a`. (이것을 `widevine_key_id`와 혼동하지 마십시오.)

* `widevine_provider` - For our purpose, always set this to `intertrust`.

* `widevine_key_id` - `key_file_path` 항목에 지정된 라이센스의 식별자입니다. 즉, 컨텐츠를 암호화하는 데 사용하는 키를 식별합니다. 이 ID 파섹

Packager 설명서에 [](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)나와 있는 바와 같이, &quot;최상의 방법은 출력 생성에 사용할 일반적인 옵션이 포함된 구성 파일을 만드는 것입니다. 그런 다음 특정 옵션을 명령줄 인수로 제공하여 출력합니다.&quot; 이 경우 Adobe의 구성 파일이 매우 완전하므로 다음과 같이 출력을 만들 수 있습니다.

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>명령줄 매개 변수가 구성 파일 매개 변수보다 우선합니다. 이 예에서는 필요한 모든 것이 구성 파일에 있지만 구성 파일에 지정된 출력 경로를 에서 재정의했습니다 `-out_path test_dash/`.

