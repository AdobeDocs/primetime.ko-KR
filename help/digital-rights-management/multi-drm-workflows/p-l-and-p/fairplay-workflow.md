---
description: DRM 워크플로우에는 컨텐츠 패키징, 콘텐츠에 대한 라이선스 제공, 자신의 비디오 애플리케이션에서 보호된 컨텐츠 재생 등이 포함됩니다. 워크플로우는 일반적으로 각 DRM 솔루션에 대해 비슷하지만 세부 사항에는 차이가 있습니다.
title: FairPlay를 위한 멀티 DRM 워크플로우
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---


# FairPlay에 대한 다중 DRM 워크플로 {#multi-drm-workflow-for-fairplay}

DRM 워크플로우에는 컨텐츠 패키징, 콘텐츠에 대한 라이선스 제공, 자신의 비디오 애플리케이션에서 보호된 컨텐츠 재생 등이 포함됩니다. 워크플로우는 일반적으로 각 DRM 솔루션에 대해 비슷하지만 세부 사항에는 차이가 있습니다.

이 멀티 DRM 워크플로우에서는 Apple FairPlay로 보호되는 HLS 콘텐츠의 설정, 패키징, 라이선스 및 재생을 진행할 수 있습니다. 또한 이 워크플로우에는 오프라인 재생 및 라이선스 회전을 구현하기 위한 선택적 지침도 포함되어 있습니다.

## FairPlay에 ExpressPlay 서비스 사용 {#enable-expressplay-service-for-fairplay}

Apple의 FairPlay DRM 솔루션을 ExpressPlay DRM 서비스와 함께 사용할 때 일부 설정이 필요합니다. 이 작업에는 Apple에서 자격 증명을 입수하고 ExpressPlay에 업로드하는 작업이 포함됩니다.

다음 단계에 따라 FairPlay 컨텐츠 보호를 위해 ExpressPlay 서비스를 활성화합니다.

1. Apple에서 자격 증명을 얻습니다.

   이러한 자격 증명은 각 서비스 공급자에 고유하게 공급됩니다. 다음 양식을 작성하여 요청해야 합니다.[https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >기본 역할에 대해 **[!UICONTROL Content Provider]**&#x200B;을 선택합니다.

   요청이 승인되면 Apple은 *FairPlay 스트리밍 배포 패키지*&#x200B;를 사용자에게 보냅니다.
1. 인증서 서명 요청을 생성합니다.

   [!DNL openssl]을 사용하여 공개/개인 키 쌍 및 CSR(인증서 서명 요청)을 생성할 수 있습니다.

   1. 키 쌍을 생성합니다.

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. CSR을 생성합니다.

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >이 단계에 대한 지침은 *FairPlay 스트리밍 배포 패키지*&#x200B;에 있지만 편의를 위해 여기에 포함됩니다. 이 프로세스에 문제가 있는 경우 *FairPlayCertificateCreation.pdf*(배포 패키지)의 지침을 확인하십시오.

1. Apple 개발자 포털을 통해 CSR을 업로드합니다.
   1. 개발 팀의 팀 에이전트는 [!DNL developer.apple.com/account]에 로그인해야 합니다.
   1. **[!UICONTROL Certificates, Identifiers & Profiles]**&#x200B;을 클릭한 다음 페이지 왼쪽 상단에 있는 **[!UICONTROL iOS, tvOS, watchOS]** 드롭다운을 선택한 다음 페이지 왼쪽의 **[!UICONTROL Certificates->Production]**&#x200B;를 클릭합니다.
   1. 새 인증서를 요청하려면 페이지 오른쪽 위에 있는 **[!UICONTROL +]** 단추를 클릭합니다. **[!UICONTROL Production]** 아래에서 **[!UICONTROL FairPlay Streaming Certificate]** 옵션을 선택합니다.

      *iOS 인증서 추가* 대화 상자가 열립니다.
   1. *iOS 인증서 추가*&#x200B;에서 단계 2.b에서 생성한 CSR 파일을 업로드하고 **[!UICONTROL Generate]**&#x200B;를 클릭합니다.

      ASK(응용 프로그램 비밀 키)가 동일한 대화 상자에 표시됩니다.
   1. ASK를 적어서 안전한 장소에 보관하세요
   1. ASK에서 키를 눌러 인증서 생성을 완료하고 **[!UICONTROL Continue]**&#x200B;을 클릭합니다.
   1. ASK를 저장했는지 확인한 후 **[!UICONTROL Generate]**&#x200B;을 클릭하여 계속합니다.

      >[!NOTE]
      >
      >ASK 복사본을 저장하고 안전하게 저장하는 것이 중요합니다. *ASK가 손상되면 FairPlay 스트리밍을 통해 더 이상 컨텐츠를 보호할 수 없습니다.* 팀에 하나의 (1) ASK만 할당됩니다. 이 값은 다시 제공되지 않으며 나중에 검색할 수 없습니다.

   1. FPS 인증서를 다운로드합니다.

      개인 키(2.a 단계)와 공개 키(이 단계에서 다운로드한 FPS 인증서)의 백업 복사본을 안전한 장소에 저장해야 합니다.
1. FairPlay 자격 증명을 사용하여 ExpressPlay 계정을 설정합니다.
   1. 3단계에서 다운로드한 인증서 이름을 살펴보겠습니다.은 [!DNL fairplay.cer]입니다.
   1. Apple Keychain 액세스 유틸리티를 사용하여 [!DNL fairplay.cer] 파일을 엽니다.
   1. 오른쪽 상단에 있는 검색 필드에 &quot; `fairplay`&quot;을 입력하여 많은 인증서를 필터링합니다.
   1. 회사의 FairPlay 인증서를 확인합니다.

      회사 이름은 Apple에서 발행한 인증서와 연결해야 합니다.
   1. 확장 화살표를 선택하여 인증서를 확장하고 개인 키를 마우스 오른쪽 단추로 클릭합니다.
   1. **[!UICONTROL Export "Your Company Name"]**&#x200B;을 선택하고 [!DNL .p12] 파일을 저장합니다.

      이 파일의 보안을 위해 암호를 할당하라는 메시지가 표시됩니다. 자격 증명 패키지와 함께 이 암호를 보내야 하므로 이 암호를 적어 두십시오.
   1. [www.expressplay.com](https://www.expressplay.com)에서 계정에 로그인합니다.
   1. 왼쪽 상단에서 **[!UICONTROL DRM SERVICES]**&#x200B;을 클릭한 다음 **[!UICONTROL FairPlay]** 탭을 선택합니다.
   1. FairPlay 자격 증명을 ExpressPlay 계정에 업로드합니다.

      1. ASK의 값을 포함하는 텍스트 파일을 만듭니다(예: 32자).`1234567890abcdef1234567890abcdef`)을 클릭하고 업로드할 이 파일을 선택합니다.
      1. 4.f 단계에서 PKCS12 파일을 선택합니다.을 참조하십시오.
      1. 4.f 단계에서 PKCS12 파일 암호를 입력합니다.
      1. [업로드] 단추를 클릭합니다.

이제 FairPlay용 ExpressPlay 서비스를 사용하여 [!DNL fairplay.cer] 인증서와 함께 FairPlay 컨텐츠 보호 기능을 사용하여 iOS 애플리케이션 또는 HTML5 페이지를 만들 수 있습니다.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### FairPlay {#package-your-content-for-fairplay}에 대한 컨텐츠 패키징

콘텐츠를 패키징하려면 Adobe Offline Packager나 ExpressPlay의 Bento4 Packager와 같은 다른 도구를 사용할 수 있습니다.

패키저에서 재생할 비디오를 준비하고(예: 원본 파일을 조각내어 매니페스트에 넣기) 선택한 DRM 솔루션을 사용하여 비디오를 보호할 수 있습니다(이 경우 FairPlay).

* [FairPlay DRM용 Adobe 오프라인 패키저](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay 패키지 - HLS용 Bento4](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. 콘텐츠를 패키징합니다.

   다음은 Adobe Offline Packager를 사용하는 패키징 예제입니다. Packager는 다음과 같은 구성 파일(예: [!DNL fairplay.xml])을 사용합니다.

   ```
   <config>
   <in_path>mp4_file_path</in_path>
   <out_type>hls</out_type>
   <out_path>out_file_path</out_path>
   <drm/>
   <drm_sys>FAIRPLAY</drm_sys>
   <frag_dur>4</frag_dur>
   <target_dur>6</target_dur>
   <key_file_path>creds/fairplay.bin</key_file_path>
   <iv_file_path>creds/iv.bin</iv_file_path>
   <key_url>user_provided_value</key_url>
   <content_id>_default_</content_id>
   </config>
   ```

   * `in_path` - 이 항목은 로컬 패키징 시스템에서 소스 비디오의 위치를 가리킵니다.
   * `out_type` - 이 항목은 패키지된 출력의 유형을 설명합니다(이 경우 FairPlay용 HLS).
   * `out_path` - 로컬 시스템에서 출력할 위치입니다.
   * `drm_sys` - 패키징하는 DRM 솔루션 이 경우 `FAIRPLAY`입니다.
   * `frag_dur` - 조각 지속 시간(초)입니다.
   * `target_dur` - HLS 출력의 대상 지속 시간입니다.
   * `key_file_path` - 패키징 시스템에서 CEK(Content Encryption Key) 역할을 하는 라이센스 파일의 위치입니다. 기본 64로 인코딩된 16바이트 16바이트 16진수 문자열입니다.
   * `iv_file_path` - 패키징 시스템에서 IV 파일의 위치입니다.
   * `key_url` - 파일 태그의 URI  `EXT-X-KEY` 매개  [!DNL .m3u8] 변수입니다.
   * `content_id` - 기본값.

   [Packager 설명서](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)에 명시된 대로 &quot;출력 생성에 사용할 일반적인 옵션이 포함된 구성 파일을 만드는 것이 좋습니다. 그런 다음 특정 옵션을 명령줄 인수로 제공하여 출력을 만듭니다.&quot;

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   생성된 M3U8 파일에는 다음과 같이 나타나는 `EXT-X-KEY` 특성이 있습니다.

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### FairPlay 정책 설정 {#setting-policies-for-fairplay}

권한 부여 서버를 사용하여 FairPlay로 보호된 콘텐츠에 대한 정책을 설정할 수 있습니다. 직접 설정을 하거나 Adobe에서 제공하는 샘플 권한 부여 서버를 사용할 수 있습니다.

Adobe은 *시간 기반* 및 *장치 바인딩* 자격 부여를 수행하는 방법을 보여주는 샘플 ExpressPlay 자격 부여 서버(SEE)를 제공합니다. 이 샘플 권한 부여 서버는 ExpressPlay 서비스의 맨 위에 구축되어 있습니다.

[참조 서버:샘플 ExpressPlay 권한 부여 서버(SEE)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [참조 서비스:시간 기반 자격 부여](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [참조 서비스:장치 바인딩 자격 부여](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## FairPlay {#licensing-and-playback-for-fairplay} 라이선스 및 재생

FairPlay로 보호된 내용의 라이선스 및 재생 기능을 사용하려면 비디오 매니페스트 파일(skd:)에 사용되는 스키마와 ExpressPlay 토큰 요청에 사용되는 스키마 간 URL 스킴을 교체해야 합니다(https:).

iOS TVSDK 클라이언트에서 라이선스 및 재생을 구현하는 방법은 다음과 같습니다.[TVSDK 응용 프로그램에서 Apple FairPlay 사용](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) 또한 선택적으로 FairPlay를 위한 오프라인 재생 및 라이선스 회전을 구현할 수 있습니다.

## FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}이(가) 있는 HLS 오프라인

플레이어가 웹(예: 비행기)에서 분리되어 웹 라이선스로부터 분리되므로 해당 라이선스를 검색할 수 없는 경우 사용자가 FairPlay로 보호된 콘텐츠를 재생할 수 있도록 할 수 있습니다.

이 작업을 시작하기 전에 Apple 문서 **&quot;FairPlay 스트리밍 및 HTTP 라이브 스트리밍을 사용한 오프라인 재생&quot;**&#x200B;을 다운로드하여 읽으십시오. TS(전송 스트림) 세그먼트를 다운로드하여 로컬 시스템에 저장하는 방법을 알아보려면 이 안내서를 읽어 보십시오.

이 워크플로우에서 FairPlay에 대한 오프라인 재생을 구현합니다.

1. HLS TS 세그먼트를 다운로드합니다.
1. FairPlay 서버에서 영구 대여 라이선스 요청(**&quot;FairPlay 영구 대여 정책&quot;** 참조)
1. `persistentContentKey`을(를) 저장합니다.
1. 오프라인 FairPlay 콘텐츠를 재생합니다.

>[!NOTE]
>
>지속적인 콘텐츠 키가 만료된 경우 클라이언트의 FairPlay 스트리밍이 암호 해독을 시작하지 않습니다. 그러나 재생 중에 컨텐츠 키가 만료되는 경우 사용자 환경은 계속 유지됩니다.
>
>자세한 내용은 [HTTP 라이브 스트리밍](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) 문서를 사용한 작업을 참조하십시오.

### FairPlay 라이선스 순환 {#section_D32AA08C61474B4F876AC2A5F18CB879}

라이선스 순환은 장기간 재생되는 컨텐츠에 대한 라이선스 해킹을 방지하기 위한 체계입니다.

M3U8 매니페스트에서 각 키 태그는 다음 키 태그까지 또는 파일의 끝까지 다음 TS 세그먼트에 적용됩니다.

라이센스 순환을 추가하려면 다음을 수행합니다.

* 라이선스 순환 시간 동안 새로운 FairPlay 키 태그를 삽입합니다.

   아무 개수의 키 태그를 추가할 수 있습니다.

   선형 내용의 경우 M3U8 창에서 최신 키 태그를 유지 관리해야 합니다. 2개의 TS 세그먼트가 남은 경우(약 20초) iOS는 다음 M3U8을 요청합니다. 새 M3U8에 새 키 태그가 포함되어 있으면 모든 주요 요청이 즉시 발생합니다. 이전 기존 키는 다시 요청되지 않습니다. iOS는 재생이 시작되기 전에 모든 주요 요청이 완료될 때까지 기다립니다.

   라이선스 회전이 있는 VOD 컨텐츠의 경우 재생 시작 시 모든 주요 요청이 발생합니다.

   다음은 키 회전이 있는 M3U8 샘플입니다.

   ```
   #EXTM3U
   #EXT-X-TARGETDURATION:10
   #EXT-X-VERSION:5
   #EXT-X-MEDIA-SEQUENCE:0
   #EXT-X-PLAYLIST-TYPE:VOD
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://one?cek=1dc2cc71d913f4f74eca0c4632
   212b25&iv=e21f0f72b6363ff6143737cb1e9ca8d7",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence0.ts
   #EXTINF:10,
   fileSequence1.ts
   #EXTINF:10,
   fileSequence2.ts
   #EXTINF:10,
   fileSequence3.ts
   #EXTINF:10,
   fileSequence4.ts
   #EXTINF:10,
   fileSequence5.ts
   #EXTINF:10,
   fileSequence6.ts
   #EXTINF:10,
   fileSequence7.ts
   #EXTINF:10,
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://two?cek=f6efc698b96cf8f4fa46d5237d
   337c77&iv=18401077091784bcda8079acf978dc95",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence8.ts
   #EXTINF:10,
   ```
