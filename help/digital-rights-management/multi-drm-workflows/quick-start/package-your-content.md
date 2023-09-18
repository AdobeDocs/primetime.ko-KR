---
description: 컨텐츠 패키징은 웹을 통해 재생할 비디오 컨텐츠를 준비하는 프로세스입니다. 패키징에는 원시 비디오를 매니페스트 파일로 변환하고, 선택적으로 서로 다른 장치 및 브라우저에 대해 서로 다른 DRM 솔루션을 사용하여 콘텐츠를 암호화하는 작업이 포함됩니다.
title: 콘텐츠 패키지
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 콘텐츠 패키지 {#package-your-content}

컨텐츠 패키징은 웹을 통해 재생할 비디오 컨텐츠를 준비하는 프로세스입니다. 패키징에는 원시 비디오를 매니페스트 파일로 변환하고, 선택적으로 서로 다른 장치 및 브라우저에 대해 서로 다른 DRM 솔루션을 사용하여 콘텐츠를 암호화하는 작업이 포함됩니다.

콘텐츠를 준비하려면 오프라인 패키지 Adobe 또는 ExpressPlay의 Bento4 패키지 프로그램과 같은 기타 도구를 사용할 수 있습니다. 패키저는 둘 다 재생을 위해 비디오를 준비하고(예: 원본 파일을 조각화하여 매니페스트에 넣기) 선택한 DRM 솔루션(PlayReady, Widevine, FairPlay, Access 등)으로 비디오를 보호합니다.:

* [Adobe 오프라인 패키지](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [익스프레스플레이 패커저](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 설정을 테스트하는 데 사용할 콘텐츠를 패키징하거나 가져옵니다.

   패키징에 대해 기억해야 할 중요한 사항 중 하나는 이 패키징 단계에서 사용하는 키 ID(콘텐츠 ID)가 후속 라이선스 토큰 요청에서 제공해야 하는 ID와 동일하다는 것입니다. Key ID는 CEK를 식별하는 유일한 항목입니다(자체 키 관리 데이터베이스에 저장되거나 [ExpressPlay의 주요 스토리지 서비스](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Adobe 액세스에 익숙한 사용자의 경우, 이는 다양한 솔루션이 작동하는 방식에 있어 중요한 차이점입니다. Access에서 라이선스 키는 DRM 메타데이터에 포함되어 있으며 보호된 콘텐츠와 함께 앞뒤로 전달됩니다. 여기에 설명된 다중 DRM 시스템에서는 실제 라이선스가 전달되지 않고 안전하게 저장되며 키 ID를 통해 획득됩니다.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

다음은 Widevine용 Offline Packager Adobe 를 사용하는 패키징 예입니다. Packager는 구성 파일(예: [!DNL widevine.xml])를 조정할 때 유용합니다.

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

* `in_path` - 이 항목은 로컬 패키징 컴퓨터의 소스 비디오 위치를 가리킵니다.
* `out_type` - 이 항목은 패키지된 출력의 유형을 설명합니다(이 경우 DASH)(HTML 5의 Widevine 보호용).
* `out_path` - 로컬 시스템에서 출력을 보낼 위치입니다.
* `drm_sys` - 패키지하는 DRM 솔루션. 다음 중 하나가 됩니다. `widevine`, `fairplay`, 또는 `playready`.

* `frag_dur` 및 `target_dur` 는 비디오 재생과 관련된 DASH 관련 지속 시간 항목입니다.

* `key_file_path` - CEK(콘텐츠 암호화 키) 역할을 하는 패키징 컴퓨터의 라이선스 파일 위치입니다. Base-64로 인코딩된 16바이트 16진수 문자열입니다.
* `widevine_content_id` - 이것은 Widevine &quot;boilerplate&quot;입니다; 그것은 항상 `2a`. (이것을 와 혼동하지 마십시오. `widevine_key_id`.)

* `widevine_provider` - For our purposes 항상 set this to `intertrust`.

* `widevine_key_id` - 다음에서 지정한 라이선스의 식별자입니다. `key_file_path` 입력. 즉, 콘텐츠를 암호화하는 데 사용하는 키를 식별합니다. 이 ID는 직접 만드는 16바이트 HEX 문자열입니다.

에 명시된 대로 [Packager 설명서](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)를 설정하는 것이 좋습니다. 출력 생성에 사용할 일반 옵션이 포함된 구성 파일을 만듭니다. 그런 다음 특정 옵션을 명령줄 인수로 제공하여 출력을 만듭니다.&quot; 이 경우 구성 파일이 상당히 완성되었으므로 다음과 같이 출력을 생성할 수 있습니다.

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>명령줄 매개 변수가 구성 파일 매개 변수보다 우선합니다. 이 예제에서 필요한 모든 것은 구성 파일에 있지만 구성 파일에 지정된 출력 경로를 `-out_path test_dash/`.
