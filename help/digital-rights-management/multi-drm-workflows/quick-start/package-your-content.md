---
description: 컨텐츠 패키징은 웹에서 재생되는 비디오 컨텐츠를 준비하는 프로세스입니다. 패키징에는 원시 비디오를 매니페스트 파일로 변환하거나 다양한 장치 및 브라우저에 맞는 다양한 DRM 솔루션을 사용하여 컨텐츠를 암호화하는 작업이 포함됩니다.
title: 콘텐츠 패키지
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# 콘텐트 패키지 {#package-your-content}

컨텐츠 패키징은 웹에서 재생되는 비디오 컨텐츠를 준비하는 프로세스입니다. 패키징에는 원시 비디오를 매니페스트 파일로 변환하거나 다양한 장치 및 브라우저에 맞는 다양한 DRM 솔루션을 사용하여 컨텐츠를 암호화하는 작업이 포함됩니다.

컨텐츠를 준비하려면 Adobe Offline Packager나 ExpressPlay의 Bento4 Packager와 같은 기타 도구를 사용할 수 있습니다. 패키지 모두 재생할 비디오를 준비하고(예: 원본 파일을 조각내어 매니페스트에 넣기), 선택한 DRM 솔루션(PlayReady, Widevine, FairPlay, Access 등)으로 비디오를 보호할 수 있습니다.:

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay 패키지](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 설치 프로그램을 테스트하는 데 사용할 콘텐트를 패키징하거나 다른 방법으로 가져옵니다.

   패키징에 대해 기억해야 하는 중요한 포인트 중 하나는 이 패키지 단계에서 사용하는 키 ID(콘텐츠 ID)가 후속 라이선스 토큰 요청에 제공해야 하는 키 ID와 동일하다는 점입니다. 키 ID는 CEK(자신의 키 관리 데이터베이스에 저장되거나 [ExpressPlay의 키 저장소 서비스](https://www.expressplay.com/developer/key-storage/)를 사용하여 저장할 수 있는 유일한 항목입니다.

   >[!NOTE]
   >
   >Adobe 액세스에 익숙한 사용자에게 이는 서로 다른 솔루션이 작동하는 방식에 있어 중요한 차이입니다. Access에서 라이센스 키는 DRM 메타데이터에 포함되고 보호된 콘텐츠와 함께 앞뒤로 전달됩니다. 여기에 설명된 다중 DRM 시스템에서는 실제 라이센스가 전달되지 않지만 키 ID를 통해 안전하게 저장하고 받습니다.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

다음은 Windows용 Adobe Offline Packager를 사용하는 패키징 예제입니다. Packager는 다음과 같은 구성 파일(예: [!DNL widevine.xml])을 사용합니다.

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

* `in_path` - 이 항목은 로컬 패키징 시스템에서 소스 비디오의 위치를 가리킵니다.
* `out_type` - 이 항목은 패키징된 출력의 유형을 설명합니다(이 경우 DASH(HTML5의 무선 보호).
* `out_path` - 로컬 시스템에서 출력할 위치입니다.
* `drm_sys` - 패키징하는 DRM 솔루션 이것은 `widevine`, `fairplay` 또는 `playready`입니다.

* `frag_dur` 비디오 재생 `target_dur` 과 관련된 DASH 특정 기간 항목입니다.

* `key_file_path` - 패키징 시스템에서 CEK(Content Encryption Key) 역할을 하는 라이센스 파일의 위치입니다. 기본 64로 인코딩된 16바이트 16바이트 16진수 문자열입니다.
* `widevine_content_id` - 이것은 위키드빈 &quot;폭탄판&quot;;항상 그렇습니다 `2a`. (`widevine_key_id`과(와) 혼동하지 마십시오.)

* `widevine_provider` - 우리의 목적을 위해, 항상 이것을 다음으로  `intertrust`설정하십시오.

* `widevine_key_id` - 항목에 지정된 라이센스의  `key_file_path` 식별자입니다. 즉, 내용을 암호화하는 데 사용하는 키를 식별합니다. 이 ID는 직접 만드는 16바이트 HEX 문자열입니다.

[Packager 설명서](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)에 명시된 대로 &quot;출력 생성에 사용할 일반적인 옵션이 포함된 구성 파일을 만드는 것이 좋습니다. 그런 다음 특정 옵션을 명령줄 인수로 제공하여 출력을 만듭니다.&quot; 이 경우 구성 파일이 매우 완전하므로 다음과 같이 출력물을 만들 수 있습니다.

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>명령줄 매개 변수가 구성 파일 매개 변수보다 우선합니다. 이 예제에서는 필요한 모든 것이 구성 파일에 있지만 구성 파일에 지정된 출력 경로를 `-out_path test_dash/`으로 재정의했습니다.

