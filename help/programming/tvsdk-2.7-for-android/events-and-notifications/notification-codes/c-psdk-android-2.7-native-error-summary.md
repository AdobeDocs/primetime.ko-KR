---
title: NATIVE_ERROR 알림에 대한 세부 사항
description: NATIVE_ERROR 알림에 대한 세부 사항
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '6888'
ht-degree: 2%

---


# NATIVE_ERROR 알림에 대한 세부 사항 {#details-for-the-native-error-notification}

TVSDK가 기본 오류를 처리하면 다음 메타데이터 키 값의 일부 또는 전체를 문자열로 반환합니다.

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 메타데이터 키 이름 </th> 
   <th colname="col2" class="entry"> 메타데이터 값 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>AVE의 기본 오류 코드입니다. </p> <p>이러한 코드는 다음과 같습니다. 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM 오류(코드 3300~3367). 동일한 Flash Player 오류 코드와 동일합니다 </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">비디오 재생 오류(-1~89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">암호화 오류(300~307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">알림에 대한 간략한 설명(예: <span class="codeph"> AAXS_InvalidVoucher</span> 또는 <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 설명</span> </td> 
   <td colname="col2"> 알림에 대한 자세한 설명(예: 광고 확인 작업이 실패함). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodenumeric 값을 문자열로 반환합니다(예: "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodeas 문자열(예:  <span class="codeph"> kECNetworkError</span>) </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 경고</span> </td> 
   <td colname="col2"> 경고에 대한 설명입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 오류</span> </td> 
   <td colname="col2"> 오류에 대한 설명입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> DRM 모듈의 사소한 오류입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> 오류에 대한 설명입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> TVSDK가 대화하려고 시도한 DRM 서버의 URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>광고 매니페스트 로드 실패</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> 로드하지 못한 내용의 URL입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">광고 유형(<span class="codeph"> MediaResource.Type</span> 열거형의 상수). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> 광고 지속 시간(밀리초)입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> 광고에 지정된 ID. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>파일 오류</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> 미디어 파일을 다운로드하는 동안 발생한 오류에 대한 설명입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> 다운로드 중인 파일의 URL. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> 매니페스트 파일 다운로드 중 발생한 오류에 대한 설명입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">조각 다운로드 중 오류 설명(예: <span class="codeph"> ts</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>오디오 트랙 오류</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> 매니페스트에 지정된 대로 로드하지 못한 오디오 트랙의 이름입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> 매니페스트에 지정된 오디오 트랙의 언어입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>검색 오류</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> 기간의 ID(정수). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>원하는 위치(밀리초)(이중). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>기타</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Auditude 오류 코드(번호). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR:DRM 값 {#section_D240082B93D34902A18C3923C1C717B3}

Adobe 비디오 엔진의 Video Encoder 인터페이스는 `NATIVE_ERROR` 메타데이터 개체에서 이러한 DRM 알림을 반환합니다.

Adobe에 DRM 오류를 보고할 때 문제 해결 지원을 위해 `NATIVE_SUBERROR_CODE` 및 `DRM_ERROR_STRING`을(를) 포함해야 합니다.

>[!TIP]
>
>이 목록은 오류에 대한 TVSDK 관련 정보를 제공합니다. 자세한 설명은 Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300)에 대한 [ActionScript 런타임 오류 ActionScript 참조를 참조하십시오.

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> NATIVE_- ERROR_CODE 메타데이터 키 값 </th> 
   <th colname="col2" class="entry"> NATIVE_ERROR_NAME 메타데이터 키의 값 </th> 
   <th colname="col3" class="entry"> 의미 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">배포자의 소프트웨어의 조치: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Google Chrome을 사용하고 Uncognito 모드이며 Flash Player 버전이 11.6보다 작은 경우 이 오류가 발생할 수 있습니다. <p>플레이어가 브라우저의 버전 번호를 확인하고 Incognito 모드를 종료하도록 권장하는 것이 좋습니다. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">라이센스를 다시 요청합니다. <p>요청이 성공하면 로그인하거나 문제 제기를 할 필요가 없습니다. 요청이 실패할 경우 오류를 일으킨 컨텐츠를 기록합니다. <span class="codeph"> subErrorId</span> 에는 라인 오류가 있습니다(있는 경우). </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">배포자가 해야 할 작업: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Flash이 11.6보다 작은 크롬 이외의 구성에서 재시도가 실패하면 패키징에 오류가 발생했을 수 있습니다. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">특정 컨텐츠와 재패키징에 문제가 있는지 확인합니다. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>서버가 클라이언트를 인증하거나 인증하지 못했습니다. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">배포자의 소프트웨어는 사용자의 자격 증명을 재설정하거나 사용자가 컨텐츠에 대한 액세스를 갖도록 안내하는 데 필요한 조치를 취해야 합니다. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">배포자는 배포자의 인증 및 인증 메커니즘이 제대로 작동하는지 확인해야 합니다. <p>배포자가 인증 또는 인증 기능을 사용할 계획이 없는 경우 해당 콘텐츠의 정책에 인증이 필요한지 여부를 확인하고 정책/라이센스 불일치 진단을 참조하십시오. </p> </li> 
    </ul> <p>이 오류 코드에 대한 자세한 내용은 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM 오류 3301 원인 및 해상도</a>를 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>Access 4.0 이상에서 이 오류는 원격 키 URL이 HTTPS를 스키마로 사용하지 않는 경우 iOS에서 발생합니다. HTTPS가 필요합니다. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">배포자가 Access v4 이전 버전을 사용하고 있거나, 4버전 이상을 사용하고 있지만, 플랫폼이 iOS가 아닌 경우, 배포자의 소프트웨어는 오류를 기록해야 합니다. <p>이 오류는 iOS에서만 발생합니다. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">배포자의 소프트웨어가 Adobe 액세스 버전 4 이상이고 플랫폼이 iOS인 경우 배포자는 HTTPS로 사용 중인 원격 키 서버 URL을 변경해야 합니다. <p>HTTP만 사용하는 경우 배포자는 HTTPS 서버를 설정해야 할 수 있습니다. 그렇지 않은 경우 배포자는 기록된 정보를 Adobe에 제출하고 문제를 제기해야 합니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>현재 보고 있는 콘텐트가 콘텐트 공급자가 설정한 규칙에 따라 만료되었습니다. subErrorId에는 클라이언트별 오류 또는 행 오류가 포함되어 있습니다. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">배포자의 소프트웨어는 만료되지 않은 새로운 라이센스를 사용할 수 있는지 여부를 결정하기 위해 서버로부터 라이센스를 다시 획득하려고 시도해야 합니다. <p>사용 가능한 라이센스가 없거나 라이센스가 만료된 경우 사용자가 새 라이센스를 취득하도록 허용하거나 내용을 볼 수 없음을 사용자에게 알립니다.만료/종료 날짜가 경과된 정책으로 콘텐트를 패키지화한 경우 라이선스 서버는 <span class="codeph"> PolicyEvaluationException</span>을 보고하고 정책 종료 날짜가 만료되었음을 나타냅니다(서버 오류 코드 303). 서버의 로그 파일을 확인하여 확인합니다. </p> <p>가능하면 패키징 중에 사용한 정책을 확인하여 만료되었는지 확인해야 합니다. Java 명령줄 도구는 다음과 같습니다. 
        <code>
         java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol
        </code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">배포자는 라이센스 만료 날짜가 의도한 대로 구성되었는지 확인해야 합니다. </li> 
     </ul> </p> <p>이 오류 코드에 대한 자세한 내용은 라이브 스트림?</a>을 사용하여 AMS/FMS의 <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303(콘텐츠 만료)을 참조하십시오. </a></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">이 오류 코드에 대한 자세한 내용은 <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM 오류 3301 원인 및 해상도</a>를 참조하십시오. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>네트워크 지연 또는 클라이언트가 오프라인이기 때문에 라이센스 또는 도메인 서버에 대한 연결 시간이 초과되었습니다. 일반적으로 subErrorId에는 HTTP 반환 코드가 포함되어 있습니다. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">배포자의 소프트웨어는 정상 작동이 확인된 서버에 대한 네트워크 연결을 시도해야 합니다. <p>시도가 실패하면 네트워크에 다시 연결하라는 메시지를 표시합니다. 성공적으로 시도하면 기록합니다. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">배포자는 사용 중인 라이센스 및 도메인 서버가 온라인 상태이며 클라이언트의 네트워크에서 볼 수 있는지 확인해야 합니다. </li> 
    </ul> <p>이 오류 코드에 대한 자세한 내용은 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] 원인 및 해상도</a>를 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Android용 최신 버전의 TVSDK 사용 <p>현재 클라이언트는 요청된 작업을 완료할 수 없지만 업데이트된 클라이언트가 요청을 완료할 수 있습니다. </p> <p>다음과 같은 몇 가지 원인이 있을 수 있습니다. 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">이 클라이언트에서 사용할 수 없는 공유 도메인이 사용되었습니다. Chrome에서는 재생이 작동하지만 다른 브라우저에서는 그렇지 않고 그 반대의 경우도 마찬가지입니다. <p> <p>팁:크롬은 다른 브라우저에서 사용하는 것과 다른 PHDS/PHLS 키를 사용합니다. 자세한 내용은 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>을 참조하십시오. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">5.0 이전의 iOS 버전에서 실행할 때 응용 프로그램에서 여러 DRMSessions를 추가하려고 합니다. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">버전 2만 지원되는 경우 메타데이터의 버전이 3 이상일 수 있습니다. </li> 
     </ul> </p> 
    <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
     <li id="li_7A83869D4262443DA35FA1DF8D3097DD">배포자의 소프트웨어는 사용자에게 경고해서 작업을 중단합니다. <p>소프트웨어의 사용 가능 여부를 결정할 수 있는 방법이 있는 경우, 사용자에게 해당 플랫폼에 적합한 방식으로 업그레이드를 지시하십시오. </p> </li> 
     <li id="li_AF9C2711FDE54DA196EB9D2864632000">공유 도메인으로 인해 문제가 발생하는 경우 배포자는 업데이트된 런타임 또는 라이브러리에 대해 Adobe에 문의해야 합니다. <p>Flash 런타임의 경우 배포자는 응용 프로그램에서 직접 업그레이드를 강제할 수 있습니다. 라이브러리의 경우 배포자는 업데이트된 라이브러리를 입수하고 애플리케이션을 다시 구축하여 사용자에게 배포해야 합니다. </p> <p>여러 DRMSession으로 인해 문제가 발생하는 경우, 배포자는 여러 DRMS를 추가하기 전에 iOS 버전 번호를 확인하기 위해 애플리케이션을 업데이트해야 합니다. 또는 응용 프로그램의 iOS v5 이상 배포를 제한할 수 있습니다. </p> <p>메타데이터 버전이 버전 2보다 높아서 문제가 발생하는 경우 메타데이터가 손상되었을 수 있습니다. 메타데이터를 다시 작성하고 결과를 볼 수 있습니다. 문제가 계속 표시되는 경우 문제를 기록하고 Adobe으로 문제를 제기하십시오. </p> </li> 
    </ul> <p>이 오류 코드에 대한 자세한 내용은 <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> 3306 DRMErrorEvent 오류 코드</a>를 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>이 취약점은 일반적으로 Adobe 액세스 코드의 버그를 나타내며 아래에 알려진 버그가 없는 경우 예상치 못한 결과입니다. subErrorId에는 클라이언트별 오류 또는 행 오류가 포함되어 있습니다. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">브라우저가 Windows의 Chrome이고 Flash 버전이 11.6(SWF 버전 19 이상)인 경우, 배포자의 소프트웨어는 사용자가 정보 제공자에서 <span class="uicontrol"> Deny</span>을 누르고 3368과 동일한 것으로 간주해야 합니다. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">브라우저가 Chrome이 아니거나 Flash 버전이 11.6이 아닌 경우 3307이 발생하는 경우, 배포자는 Adobe으로 에스컬레이션해야 합니다. </li> 
    </ul> <p>중요:<span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span>은(는) Chrome 브라우저 버전 24-28에서 발생할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>이 오류는 사용 중인 라이선스에 콘텐트의 암호를 해독하는 데 잘못된 키가 포함될 때마다 발생합니다. subErrorId에는 클라이언트별 오류 또는 행 오류가 포함되어 있습니다. </p> <p>이 버그를 생성하는 방법은 두 가지뿐입니다. 
     <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
      <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">고객이 라이선스 생성을 위한 표준 Adobe 도구(예: 라이센서 서버 Java 프레임워크)를 수정했습니다. <p>이 경우 라이센스에 컨텐츠에 해당되지 않을 수 있는 잘못된 키가 포함되어 있습니다. </p> </li> 
      <li id="li_21D04ED1F1FA464785BC297D385766FF">고객은 동일한 라이선스 ID를 가진 여러 개의 라이선스를 발급했습니다. <p>이 경우, 클라이언트에서 컨텐츠 메타데이터와 일치하는 여러 개의 라이선스를 사용할 수 있으며 액세스 코드가 잘못된 라이선스를 선택하여 사용할 수 있습니다. </p> </li> 
     </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">배포자의 소프트웨어는 서버로부터 라이센스를 재취득하려고 시도해야 합니다. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">사용 가능한 라이센스가 없거나 라이센스가 만료된 경우 사용자가 새 라이센스를 획득할 수 있는 작업 과정을 제공하거나 컨텐츠를 볼 수 없다는 내용을 사용자에게 알리고 문제를 기록합니다. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">AIR용 도메인 바인딩된 내용일 경우 사용자가 도메인에 가입할 수 있는 방법을 제공합니다. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">배포자는 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">액세스 라이센스 서버의 라이센스 발급 부분을 사용자 지정하지 않았는지 확인합니다. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">모든 라이선스에 대해 고유한 라이선스 ID를 발급하는지 확인합니다. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Adobe으로 문제를 제기합니다. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader  </span> </td> 
   <td colname="col3"> <p>헤더가 65,536바이트보다 클 경우 발생합니다. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">배포자의 소프트웨어는 오류를 일으킨 컨텐츠를 기록해야 합니다. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">배포자는 특정 컨텐츠가 있는 경우 오류가 재현될 수 있음을 확인해야 합니다. 끊어진 콘텐츠를 재패키징합니다. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch  </span> </td> 
   <td colname="col3">Android 응용 프로그램이 사용 중인 응용 프로그램과 일치하지 않습니다. <p>올바른 AIR 응용 프로그램 또는 Flash SWF를 사용하지 않습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch  </span> </td> 
   <td colname="col3"> 사용하지 않음. 이 문제는 AIR의 버전 1.x 스택에 의해 계속 발생할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity  </span> </td> 
   <td colname="col3"> 이 문제를 해결하려면 서버에서 라이센스를 다시 다운로드하십시오. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed  </span> </td> 
   <td colname="col3"> <p>이 문제는 시스템이 파일 시스템에 쓸 수 없을 때 발생합니다. <span class="codeph"> subError</span> 클라이언트 특정 오류 또는 행 오류를 포함합니다. </p> <p>Microsoft Windows에서 암호화된 내용에 너무 긴 licenseID 또는 policyID가 있는 경우 Active X 또는 NPAPI 플러그인 플래시 플레이어에서 오류 3313이 발생할 수 있습니다. Windows의 최대 경로 길이 때문입니다. (Pepper 플러그인에는 이 문제가 없습니다.) </p> <p>왓슨 3549660 보기 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">배포자의 소프트웨어는 사용자에게 사용자 디렉토리가 잠기지 않았는지, 전체 또는 잠겨 있는 볼륨에 있는지 확인하라는 메시지를 표시해야 합니다. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">배포자가 Flash이 아닌 AIR를 사용하는 경우 경로 길이 제한으로 인해 문제가 발생할 수 있습니다. <p>유통업체들은 그들의 AIR 응용 프로그램의 이름을 합리적인 것으로 단축해야 한다. 또한 보다 짧은 <span class="codeph"> licenseID</span> 및 <span class="codeph"> policyID</span>로 컨텐츠를 다시 게시합니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata  </span> </td> 
   <td colname="col3"> <p>이 오류는 종종 컨텐츠가 테스트 PKI 인증서로 패키지되었고 플레이어가 프로덕션 PKI로 빌드되었음을 나타냅니다. subErrorId에는 클라이언트별 오류 또는 행 오류가 포함되어 있습니다. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">배포자의 소프트웨어는 오류를 일으킨 컨텐츠를 기록해야 합니다. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">배포자는 오류가 특정 컨텐츠가 재생산될 수 있는지 확인해야 합니다. <p>깨진 콘텐츠를 다시 패키징해야 할 수도 있습니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied  </span> </td> 
   <td colname="col3"> <p>3305를 의도할 때 이 오류 코드가 발생하는 알려진 버그가 있습니다. 자세한 내용은 <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] 원인 및 해상도</a>를 참조하십시오. </p> <p>AIR에서 로드한 원격 SWF는 Flash Access 기능에 액세스할 수 없습니다. 네트워크 액세스 중에 보안 오류가 발생하는 경우에도 이 오류 코드를 실행할 수 있습니다. 예를 들어 crossdomain.xml을 사용하여 연결할 클라이언트가 대상 서버가 아니거나 crossdomain.xml에 연결할 수 없는 문제가 있습니다. </p> <p>자세한 내용은 <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM 오류 3315의 가능한 루트 원인 및 해상도</a>를 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED  </span> </td> 
   <td colname="col3"> <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>입니다. Flash 오류 코드와 충돌하여 3344로 이동했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFfailed  </span> </td> 
   <td colname="col3"> <p>중요: 이는 드문 오류이며 일반적으로 제작 환경에서 발생하지 않습니다. </p> <p>오류가 발생하면 다음 중 하나를 수행할 수 있습니다. 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">AIR를 사용하는 경우 다시 설치합니다. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Flash Player을 사용하는 경우 <span class="codeph"> AdobeCP</span> 모듈을 다시 다운로드합니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion  </span> </td> 
   <td colname="col3"> Android에는 적용되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI  </span> </td> 
   <td colname="col3"> Android에는 적용되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed  </span> </td> 
   <td colname="col3"> Android에는 적용되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15n실패  </span> </td> 
   <td colname="col3"> <p>키를 사용하여 클라이언트를 프로비저닝하는 프로세스가 실패했습니다. subErrorId에는 클라이언트별, 서버별 또는 라인 오류가 포함됩니다. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">배포자의 소프트웨어는 최소 한 번 작업을 다시 시도해야 합니다. <p>Windows에서 Google Chrome을 사용하는 경우 샌드박스에 없는 플러그인 액세스를 허용하는 방법에 대한 설명을 제공합니다. 자세한 내용은 <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome의 샌드박스 해제 액세스가 거부됨</a>을(를) 참조하십시오. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">배포자는 다음 작업 중 하나를 완료해야 합니다. 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">모든 플랫폼에서 오류가 일관되면 Adobe으로 문제를 제기해야 합니다. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Windows의 Chrome에만 오류가 있는 경우 샌드박스 없는 플러그인 액세스를 허용하도록 사용자에게 안내하십시오. </li> 
      </ul> <p>배포자는 SWF를 버전 19 이상으로 업데이트해야 하며 Chrome 관련 3321 오류인 3368 오류가 발생합니다. 오류 3368은 배포자의 소프트웨어에 의해 더욱 구체적으로 처리될 수 있습니다. 이 변경 사항은 Chrome Stable 채널 버전 26.0.1410.43에서 도입되었습니다. </p> <p>팁:<span class="codeph"> 3321:1090519056</span> 오류가 Flash Player 버전 11.1에서 11.6으로 발생할 수 있습니다. 최신 Flash Player 버전으로 업그레이드하는 것이 좋습니다. </p> </li> 
    </ul> <p>자세한 내용은 <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM 오류 3321 원인 및 해상도</a>를 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>글로벌 스토어 손상 오류</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed  </span> </td> 
   <td colname="col3"> <p>장치가 초기화될 때 있었던 구성과 일치하지 않는 것으로 나타납니다. subErrorId에는 클라이언트별 또는 라인 오류가 포함됩니다. </p> <p>배포자의 소프트웨어는 다음 작업 중 하나를 완료해야 합니다. 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>장치가 Flash Player을 사용하고 있지 않고 AIR, iOS 등을 사용 중인 경우 <span class="codeph"> DRMManager.resetDRMVouchers()</span>을(를) 호출합니다. </p> <p>개발 단계에서 iOS에서 문제가 발생하는 경우 개발자에게 제3자, 시험판 배포 시스템(예: 하키 앱)에서 다운로드한 빌드와 Xcode의 로컬 빌드를 전환할 때 문제가 관찰되는지 확인하십시오. 하키 앱에서 배포된 빌드와 Xcode에서 빌드를 전환할 때 이전 설치 속성을 완전히 덮어쓰지 않습니다. 이 경우 3322 오류가 발생할 수 있습니다. </p> <p>이 문제를 해결하려면 새 빌드를 설치하기 전에 개발자가 장치에서 이전 빌드를 제거해야 합니다. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">장치가 Flash Player을 사용하고 있고 3322 또는 3346 오류 코드에서 사용할 수 없는 경우 Chrome의 <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> DRM 오류 3322/3346/3368(Info-Bar 문제)</a>에서 DRM 라이선스 저장소를 프로그래밍 방식으로 재설정하는 방법에 대한 Adobe 지침을 참조하십시오. </li> 
     </ul> </p> <p>이 오류는 자주 발생하지 않을 것으로 예상됩니다. 로밍 프로필을 사용하는 회사 환경에서 사용자가 DRM으로 보호되는 콘텐츠를 보고 있는 경우 사용자가 다른 컴퓨터에서 로그인하면 오류가 3322일 수 있습니다. 가능한 경우, 배포자는 사용자로부터 이 정보를 얻으려고 노력해야 합니다. </p> <p>오류가 자주 발생하는 경우 Adobe으로 전달됩니다. 라이선스 스토어를 재설정하여 문제를 해결했는지 여부를 Adobe에 통보하고 오류가 발생하는 브라우저에 대해 Adobe에 알려야 합니다. </p> <p>자세한 내용은 다음 문서를 참조하십시오. 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore  </span> </td> 
   <td colname="col3"> <p>DRM 클라이언트에서 사용하는 파일이 예기치 않게 수정되었습니다. subErrorId에는 클라이언트별 또는 라인 오류가 포함됩니다. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">배포자의 소프트웨어는 3322와 같은 방식으로 사용자에게 재설정을 안내해야 합니다. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">GlobalStore가 사용자 기반 하드 드라이브의 예상 실패율보다 높은 비율로 실패하는 경우, 문제를 Adobe으로 제기하십시오. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid  </span> </td> 
   <td colname="col3"> 이 응용 프로그램의 DRM 로컬 저장소를 다시 설정합니다. DRMManager.resetDRM을 호출합니다. <p>라이선스 서버에서 CRL(인증서 해지 목록) 서버에 연결하여 CRL 파일을 새로 고칠 수 없거나 클라이언트 컴퓨터에서 라이선스 서버에서 해지한 라이선스/인증을 요청할 수 있습니다. </p> <p>서버 로그에서 오류 코드 111은 MachineTokenInvalid입니다. 그러나 클라이언트 수준에서 오류 코드 111은 오류 코드 3324로 변환됩니다. </p> <p>DRM 라이선스 서버 관리자는 고객의 라이선스 서버에서 Adobe CRL 파일을 검색할 수 있는지 여부를 확인해야 합니다. 고객이 Tomcat을 사용하는 경우 고객은 <span class="filepath"> tomcat/temp/</span> 디렉토리를 확인하여 4개의 CRL 파일이 있는지 여부를 확인할 수 있습니다. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
     <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">파일이 이 디렉토리에 있는 경우 Windows 탐색기와 CRL 뷰어 응용 프로그램에서 파일을 두 번 클릭하여 파일이 만료되었는지 확인합니다. </li> 
     <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">tomcat/temp/에 파일이 없는 경우, 방화벽/라우팅 문제로 인해 이 라이센스 서버가 Adobe CRL 서버에 도달할 수 없는 것으로 간주할 수 있습니다. </li> 
    </ul> <p>자세한 내용은 <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> 방화벽 규칙</a>을 참조하십시오. </p> <p>CRL 파일을 사용할 수 없거나 만료된 경우 라이센스 서버에 도달할 수 있는지 여부를 확인해야 합니다. 고객의 라이센스 서버에서 네트워크 스니퍼를 열고 서버를 다시 시작하고 서버에서 라이센스를 요청하도록 클라이언트가 시도합니다. 네트워크 트래픽을 관찰하여 다음 URL 끝점에 대한 호출이 성공했는지 여부를 확인할 수 있습니다. <p>팁: 브라우저에 다음 CRL URL을 입력하여 각 파일을 수동으로 다운로드할 수 있는지 여부를 확인할 수도 있습니다. </p> 
     <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
     </ul> </p> <p>방화벽 규칙이 열려 있고 현재 3324 오류가 없는 경우 임시 네트워크 문제가 있을 수 있습니다. 라이선스 서버에서 인증서 해지 목록을 가져오려고 할 때 오류가 발생했는지 확인하려면 <span class="codeph"> /tomcat/logs/</span> 디렉터리에 있는 고객의 서버 로그를 확인하십시오. <p>중요: CRL 파일을 갱신하는 경우 클라이언트의 많은 수(또는 버스트)가 3324 오류를 임시 네트워크 문제로 보고하는 경우 오류가 발생할 수 있습니다. 네트워크 문제가 해결되면 3324 문제도 해결되었습니다. </p> </p> <p>모든 CRL 파일 4개가 <span class="filepath"> tomcat/temp/</span> 디렉토리에 있고 클라이언트가 여전히 3324 오류 코드를 얻고 있는 경우 CRL 파일에 대한 파일 액세스 문제가 있을 수 있습니다. 이 문제를 해결하려면 로그를 검토하고 기존 CRL 파일을 삭제할 수 있습니다. </p> <p>서버 문제가 없는 경우 3322에 설명된 대로 사용자에게 재설정하라는 메시지를 표시합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>서버 저장소 손상 오류</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3325년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore  </span> </td> 
   <td colname="col3"> <p>DRM 클라이언트에서 사용하는 파일이 예기치 않게 수정되었습니다. <span class="codeph"> subError</span> 클라이언트 특정 또는 라인 오류를 포함합니다. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">AdobeCP가 문제가 되는 서버 스토어를 내부적으로 삭제했으므로 배포자의 소프트웨어가 다시 작업을 시도해야 하며 다시 시도해야 합니다. 재시도가 실패하면 문제를 기록합니다. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">사용자 기반 하드 드라이브의 예상 실패율보다 높은 비율로 재시도가 실패하면 이 문제를 Adobe으로 제기하십시오. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected  </span> </td> 
   <td colname="col3"> <span class="codeph"> DRMManager.resetDRM</span>을(를) 호출합니다. <p>라이선스 저장소가 무단/손상되었으며 더 이상 사용할 수 없습니다. </p> <p>배포자의 소프트웨어는 3322에 설명된 것과 동일한 방법으로 사용자에게 재설정을 안내해야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected  </span> </td> 
   <td colname="col3"> 시계를 수정하거나 <span class="codeph"> Authn/Lic/Domain</span> 라이센스를 다시 획득합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>인증/라이센스/도메인 서버 오류</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3328년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAgain  </span> </td> 
   <td colname="col3"> <p>서버가 클라이언트의 요청을 완료할 수 없는 서버측 오류입니다. 이 오류는 예를 들어 서버가 사용 중일 때, HTTP/500, 서버에 요청을 해독하는 데 필요한 키가 없을 때 발생할 수 있습니다. </p> <p>고객의 입장에서는 무엇이 잘못되었는지 알 방법이 없다. 고객은 일반적으로 <span class="codeph"> AdobeFlashAccess.log</span>라고 하는 Adobe 액세스 서버 로그를 검토하여 잘못된 내용을 확인해야 합니다. 문제를 나타내는 설명형 스택 추적은 항상 로그에 있습니다. <span class="codeph"> subError</span> 서버 전용 또는 행 오류를 포함합니다. </p> <p>배포자는 이 오류를 전송하는 서버를 식별하기 위해 서버 로그를 확인해야 합니다. 하위 오류 코드 101이 있는 3328 오류에 대해 서버는 요청을 해독할 수 없습니다. 고객은 라이센스 서버에 설치된 라이센스/전송 서버 인증서가 일치하는지 확인하고 패키징 중에 사용된 인증서와 일치하는지 확인해야 합니다. </p> <p>또한 고객이 참조 구현을 사용하고 있는 경우 기본 및 추가 인증서가 지정된 <span class="codeph"> flashaccess-refimpl.properties</span> 파일에 오타가 없는지 확인해야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError  </span> </td> 
   <td colname="col3"> <p>응용 프로그램별 하위 오류 코드는 Flash Access에 알려지지 않습니다. <span class="codeph"> subError</span> 게시자 사용자 지정된 라이센스 서버의 서버 특정 오류를 포함합니다. 서버에서 응용 프로그램 특정 네임스페이스에 오류를 반환했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication  </span> </td> 
   <td colname="col3"> <p>이 오류는 라이센스가 부여되기 전에 클라이언트에 인증을 요청하도록 컨텐츠가 구성되어 있을 때 발생합니다. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">배포자의 소프트웨어는 사용자를 인증한 다음 라이센스를 다시 취득해야 합니다. <p>서비스에서 인증을 사용하지 않을 경우 이 오류를 일으키는 컨텐츠의 ID를 기록합니다. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">컨텐츠가 인증이 필요하도록 구성되지 않아야 하므로 이 오류는 에스컬레이션이 필요하지 않습니다. <p>이 경우 문제가 있는 컨텐츠를 적절한 정책으로 재패키징합니다. 콘텐트가 올바르게 패키징된 경우 정책/라이센스 불일치 진단을 참조하십시오. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>위에서 다루지 않은 라이센스 실행 오류</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3331년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid  </span> </td> 
   <td colname="col3"> <p>취득한 라이선스는 아직 유효하지 않습니다. 이 문제를 해결하려면 클라이언트 클럭이 올바르게 설정되지 않았는지 확인하십시오. 클라이언트 시계를 설정하려면 컨텐츠를 재패키징하거나 라이센스 서버 구성을 수정합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired  </span> </td> 
   <td colname="col3"> 서버에서 라이센스를 다시 획득합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired  </span> </td> 
   <td colname="col3"> <p>정책이 만료될 때까지 이 컨텐츠를 재생할 수 없다는 사실을 사용자에게 알려야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform  </span> </td> 
   <td colname="col3"> <p>예를 들어 콘텐츠 공급자가 플랫폼의 Adobe 액세스를 거부하도록 Adobe 액세스를 구성했거나 공유 도메인 바인딩 라이센스가 다른 파티션을 위한 공유 도메인 토큰에 바인딩되기 때문에 이 플랫폼을 사용하여 콘텐츠를 재생할 수 없습니다. </p> <p>적절한(CDM 기능 제한) 패키지 인증을 사용하여 콘텐츠를 패키지하지 않은 경우 CDM에서 이 오류를 발생할 수 있습니다. </p> <p>내용이 잘못된 PHDS/PHLS 인증서로 패키지화된 경우, 컨텐츠는 크롬에서는 작동하지만 다른 브라우저에서는 작동하지 않을 수 있습니다(또는 그 반대). <p>팁: 이는 Chrome에서 다른 PHDS/PHLS 인증서를 사용하기 때문입니다. </p>사용 중인 인증서를 확인하려면 콘텐츠 메타데이터의 세부 정보를 덤프하고 <i>수신자 인증서</i>를 찾습니다. 자세한 내용은 <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>을 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion  </span> </td> 
   <td colname="col3"> Android용 TVSDK 최신 버전으로 업그레이드하십시오. <p>이 문제를 해결하려면 다음 작업 중 하나를 완료하십시오. 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">AIR 업그레이드 </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">Flash Player의 경우 AdobeCP 모듈을 업그레이드하고 재생을 다시 시도하십시오. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform  </span> </td> 
   <td colname="col3"> <p>예를 들어, 컨텐트 공급자가 플랫폼에서 FP/AIR에 대한 컨텐트를 거부하도록 액세스를 구성했기 때문에 이 플랫폼을 사용하여 내용을 재생할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion  </span> </td> 
   <td colname="col3"> Android용 TVSDK 최신 버전으로 업그레이드하십시오. <p>이 문제는 컨텐츠 또는 서버가 특정 버전의 Flash 또는 AIR 런타임으로의 재생을 거부하도록 구성된 경우 발생합니다. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">사용자가 Flash을 업그레이드할 수 있는 운영 체제에 있는 경우, 배포자의 소프트웨어는 사용자에게 Flash을 업그레이드하라는 메시지를 표시하고 다시 시도하십시오. 그렇지 않으면 사용자에게 다른 컴퓨터를 사용하도록 알립니다. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">3337s 오류가 의심되는 경우 특정 컨텐츠에 대해 오류가 발생하는지 확인하고 해당 컨텐츠를 재패키징합니다. 콘텐트가 올바르게 패키징된 경우 정책/라이센스 불일치 진단을 참조하십시오. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType  </span> </td> 
   <td colname="col3"> <p>연결 유형을 감지할 수 없으며 정책을 사용하려면 출력 보호를 설정해야 합니다. 이 문제는 내용이 디지털 또는 아날로그 출력 보호를 위해 패키지화된 경우에만 발생할 수 있습니다. </p> <p>버전 11.8.800.168 이전 버전의 Flash Player에서 컨텐트 보호가 <span class="codeph"> USE IF AVAILABLE</span>임을 표시한 컨텐츠에 때때로 오류 3338이 발생하는 문제가 발생했습니다. 이 문제는 버전 11.8.800.168 이상에서 해결되었습니다. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">배포자의 소프트웨어는 출력 보호가 필요하지 않은 컨텐트(예: HD 스트림의 SD 변형)의 변형을 선택합니다. <p><span class="codeph"> USE_IF_AVAILABLE </span> 컨텐츠에서 3338 오류가 발생하는 경우 플레이어 버전 번호를 확인하십시오. 플레이어 버전이 11.8.800.168 미만인 경우 사용자에게 Flash Player을 업그레이드하도록 알립니다. 3338 오류가 11.8.800.168 이상 버전에서 발생하는 경우 오류가 발생한 내용을 기록합니다. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">배포자는 이 오류가 발생하는 컨텐츠를 확인하고 내용의 정책이 아날로그 및 디지털 출력에 대해 <span class="codeph"> NO_PROTECTION</span> 또는 <span class="codeph"> USE_IF_AVAILABLE</span>을(를) 설정하고 있는지 확인해야 합니다. <p>내용이 실수로 <span class="codeph"> NO_OUTPUT</span> 또는 <span class="codeph"> REQUIRED</span>로 패키지된 경우 콘텐트를 다시 패키지하십시오. 콘텐트가 올바르게 패키징된 경우 정책/라이센스 불일치 진단을 참조하십시오. 그렇지 않으면 Adobe으로 전달됩니다. </p> </li> 
    </ul> <p>자세한 내용은 DRM 정책이 USE_IF_AVAILABLE?</a> DRM 정책이 USE_IF_AVAILABLE으로 설정된 경우 <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> 예기치 않은 3338 오류 가져오기를 참조하십시오. </a></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed  </span> </td> 
   <td colname="col3"> 아날로그 장치에서 재생할 수 없습니다. 문제를 해결하려면 디지털 장치를 연결합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvailable  </span> </td> 
   <td colname="col3"> 연결된 아날로그 외부 디스플레이 장치(모니터/TV)에 올바른 기능이 없으므로 컨텐츠를 재생할 수 없습니다(예: 장치에 Macrovision 또는 ACP가 없음). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed  </span> </td> 
   <td colname="col3"> 디지털 장치에서 콘텐츠를 재생할 수 없습니다. <p>중요: 컨텐츠 퍼블리셔는 디지털 재생을 허용하지 않아야 하므로 제작 환경에서는 이 문제가 발생하지 않아야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvailable  </span> </td> 
   <td colname="col3"> 연결된 디지털 외부 디스플레이 장치(모니터/TV)에 올바른 기능이 없습니다. 예를 들어 장치에 HDCP가 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed  </span> </td> 
   <td colname="col3"> <p>Android에는 적용되지 않습니다. </p> <p>이 오류는 현재 새 Flash 버전이 릴리스된 후에 처음 발생하는 것으로 알려져 있습니다. Flash이 열려 있는 동안 Flash이 업그레이드되어 브라우저가 다시 시작될 때까지 Flash이 잘못된 상태로 설정되기 때문에 발생합니다. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">배포자의 소프트웨어는 다음 작업을 완료해야 합니다. 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">모든 브라우저를 닫거나 종료한 다음 다시 여는 것이 좋습니다. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Flash 버전이 최신인지 확인합니다. <p>버전이 최신 버전이 아닌 경우 고객에게 업그레이드를 권장하고 브라우저의 모든 탭을 닫은 후 다시 여십시오. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">브라우저를 다시 시작한 후 오류가 발생한 것으로 나타나면 Adobe으로 전달됩니다. <p>새 버전이 릴리스되면 Adobe 지원에 문의하여 백그라운드 업데이트 문제가 해결되었는지 확인하는 것이 좋습니다. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule  </span> </td> 
   <td colname="col3"> Android에는 적용되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError  </span> </td> 
   <td colname="col3"> <p>Android에는 적용되지 않습니다. </p> <p>이 오류는 Flash 또는 AIR의 일부가 올바르게 설치되지 않은 경우에 발생합니다. </p> <p>배포자의 소프트웨어는 다음 중 하나를 수행해야 합니다. 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">사용자에게 AIR를 제거하고 다시 설치하도록 요청합니다. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">Flash Player의 경우 <span class="codeph"> System.update</span>로 전화하십시오. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed  </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">배포자의 소프트웨어는 다음 중 하나를 수행해야 합니다. 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">AIR의 경우 <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">오류 3322 또는 3346 오류 코드로 인해 Flash을 사용할 수 없는 경우 사용자는 <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> Adobe 문서의 지침에 따라 프로그래밍 방식으로 DRM 라이선스 저장소를 재설정해야 합니다. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">이 오류가 자주 발생하는 경우, 배포자는 주파수 플레이어 버전과 브라우저 버전에 대한 세부 정보를 Adobe에 제공해야 합니다. </li> 
    </ul> <p>자세한 내용은 다음 포럼 아티클을 참조하십시오. 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> 크롬의 DRM 오류 3322/3346/3368(정보-막대 문제)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 하드웨어 변경 후 3322 또는 3346 오류</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompleteDeviceCapabilities  </span> </td> 
   <td colname="col3"> <p>이 오류의 주된 의미는 라이센스에 클라이언트의 DRM 인증서가 채울 수 없음을 나타내는 제약 조건이 있다는 것입니다. 클라이언트 DRM 인증서가 발급될 때 다음 "하드웨어 기능"이 정의됩니다. 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>사용자가 액세스할 수 없는 버스</b>. <b>true</b>인 경우 암호를 해독하는 미디어가 버스를 통과하거나 응용 프로그램이 액세스할 수 있는 기본 메모리로 전혀 유입되지 않습니다. <p><b>false</b>인 경우 암호 해독 후 응용 프로그램에서 콘텐트에 액세스할 수 있습니다. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>트러스트의 하드웨어 루트입니다</b>. <b>true</b>인 경우 장치에서 부팅 시 로드되는 모든 소프트웨어가 하드웨어에서만 사용할 수 있는 키 또는 다이제스트에 대해 유효성이 검사되었습니다. <p>클라이언트에 대한 DRM 인증서에 대해 라이센스가 열리고 오류가 즉시 발생하는 경우 두 제약 조건 모두 클라이언트측에서 확인됩니다. 라이센스를 발급하기 전에 서버 측에서 이러한 제한 사항을 확인할 수도 있습니다. </p> </li> 
     </ul> </p> <p>이 오류의 두 번째 의미는 라이센스에 "Jailbreak Enforcement" 정책 세트가 있고 장치에서 탈옥이 감지되었다는 것입니다. 이 검사는 클라이언트측에서 정기적으로 수행되며 서버측에서 확인할 수 없습니다. </p> <p>배포자는 정책을 업데이트하고 제한 사항을 제거할 수 있습니다. 장치 기능 정책의 경우 <span class="codeph"> -devCapabilitiesV1</span> 플래그와 인수 없이 정책 업데이트 명령을 실행합니다. 강제 집행의 경우 <span class="codeph"> policy.enforceJailbreak=false</span>를 설정합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired  </span> </td> 
   <td colname="col3"> 하드 스톱 간격이 만료되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh  </span> </td> 
   <td colname="col3"> 서버가 클라이언트에서 지원하는 가장 높은 버전보다 높은 버전에서 실행 중입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow  </span> </td> 
   <td colname="col3"> 서버가 클라이언트에서 지원하는 최소 버전보다 낮은 버전에서 실행 중입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid  </span> </td> 
   <td colname="col3"> 도메인 토큰이 잘못되었습니다. 이 문제를 해결하려면 도메인에 다시 등록하십시오. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld  </span> </td> 
   <td colname="col3"> 도메인 토큰이 라이선스에 필요한 토큰보다 오래되었습니다. 문제를 해결하려면 도메인에 다시 등록하십시오. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew  </span> </td> 
   <td colname="col3"> 도메인 토큰이 라이선스에 필요한 토큰보다 최신입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired  </span> </td> 
   <td colname="col3"> 도메인 토큰이 만료되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed  </span> </td> 
   <td colname="col3"> 도메인 조인에 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoResponsiveRoot  </span> </td> 
   <td colname="col3"> V3 리프 라이선스의 루트 라이선스를 찾을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense  </span> </td> 
   <td colname="col3"> 포함된 유효한 라이선스를 찾을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvailable  </span> </td> 
   <td colname="col3"> 연결된 아날로그 장치에 ACP 보호가 없으므로 재생할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvailable  </span> </td> 
   <td colname="col3"> 연결된 아날로그 장치에 CGMS-A 보호가 없으므로 재생할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired  </span> </td> 
   <td colname="col3"> 콘텐츠에 도메인 등록이 필요합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain  </span> </td> 
   <td colname="col3"> 지정된 메타데이터에 대해 컴퓨터가 도메인에 등록되어 있지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError  </span> </td> 
   <td colname="col3"> 비동기 작업이 <span class="codeph"> maxOperationTimeout</span>보다 오래 걸렸습니다. iOS DRMNative Framework에서만 반환됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError  </span> </td> 
   <td colname="col3"> 전달된 M3U8 재생 목록에서 지원되지 않는 내용이 있습니다. iOS DRMNative Framework에서만 반환됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId  </span> </td> 
   <td colname="col3"> <p>프레임워크에서 장치 ID를 요청했지만 반환된 값이 비어 있습니다. </p> <p>사용자는 Chrome 설정에서 보호된 콘텐츠에 대한 <span class="uicontrol"> 식별자 허용 확인란을 선택하지 않아야 합니다.</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed  </span> </td> 
   <td colname="col3"> <p>이 브라우저/플랫폼 조합은 Uncognito 모드에서 DRM으로 보호된 재생을 허용하지 않습니다. </p> <p>배포자의 소프트웨어는 사용자가 Uncognito 모드를 종료하거나 다른 브라우저를 사용할 것을 권고해야 합니다. 자세한 내용은 <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM 오류 3365 원인 및 해상도</a>를 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter  </span> </td> 
   <td colname="col3"> <p>잘못된 매개 변수를 사용하여 액세스 라이브러리를 호스트 런타임에서 호출했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature  </span> </td> 
   <td colname="col3"> m3u8 매니페스트 서명에 실패했습니다. iOS DRMNative Framework 또는 AVE에서만 반환됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>사용자가 작업을 취소하거나 시스템에 액세스할 수 없는 설정을 입력했습니다. </p> <p>이 오류는 SWF 버전이 19 이상일 때만 발생합니다. 이전 버전과의 호환성을 위해 SWF가 버전 18 이하일 때 3321이 발생합니다. </p> <p>배포자의 소프트웨어는 샌드박스 형태의 플러그인 액세스를 허용하는 방법에 대한 설명을 사용자에게 안내해야 합니다. 자세한 내용은 Google Chrome의 샌드박스 액세스가 거부됨</a> 및 Chrome의 <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM 오류 3322/3346/3368(Info-Bar 문제)</a>을(를) 참조하십시오.<a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> </a></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>필요한 브라우저 인터페이스를 사용할 수 없습니다. 이 문제는 Pepper에서만 발생합니다. Flash 플러그인과 브라우저 버전이 일치하지 않을 수 있습니다. </p> <p>배포자의 소프트웨어는 최신 버전의 브라우저가 설치되어 있는지 사용자에게 안내해야 합니다. </p> <p> 이 오류의 발생 횟수가 증가하고, 실행 중인 브라우저 업데이트에 해당하는 경우 Adobe으로 전달됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>사용자가 <span class="uicontrol"> 보호된 콘텐츠에 대한 식별자 허용</span> 설정을 비활성화했습니다. </p> <p>팁: 이 오류는 Pepper 버전 13.0.0.x 이상에서 발생했습니다. </p> <p>배포자의 소프트웨어는 사용자에게 <span class="uicontrol"> 보호된 콘텐츠에 대한 식별자 허용</span> 설정을 사용하도록 안내해야 합니다. </p> <p>배포자의 작업 팀은 보호된 내용</span> 설정에 대해 <span class="uicontrol"> 식별자 허용 설정을 사용하도록 사용자를 안내해야 합니다. </span></p> <p>자세한 내용은 <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>을 참조하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_</span><span class="codeph"> NoOPConstrintInPixelConstraints</span> </td> 
   <td colname="col3"> <p>라이센스의 출력 보호 제약 조건에 따른 잘못된 해상도 </p> <p>배포자의 소프트웨어에 오류 메시지가 표시됩니다. 사용자에게 컨텐츠 제목으로 배포자에게 문제를 보고하도록 요청합니다. </p> <p>배포자는 유효한 정책으로 콘텐트를 다시 패키지화해야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372년 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargeThanMaxResolution</span> </td> 
   <td colname="col3"> <p>내용의 해상도가 출력 보호 제약 조건에 지정된 최대 해상도보다 큽니다. </p> <p>배포자의 운영 팀이 로그에 이 오류가 표시되는 경우 해상도 기반 출력 보호 정책을 검토하고 필요한 경우 컨텐츠를 다시 패키지해야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargeThanConstrain</span> </td> 
   <td colname="col3"> <p>내용의 해상도가 현재 활성 출력 보호 제약 조건에 의해 지정된 해상도보다 큽니다. </p> <p>배포자의 운영 팀이 로그에 이 오류가 표시되는 경우 해상도 기반 출력 보호 정책을 검토하고 필요한 경우 컨텐츠를 다시 패키지해야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>요청 생성, 응답 처리, 잘못된 인증 토큰 등 클라이언트 측 통신 처리 중에 실패했습니다. </p> <p>배포자의 운영 팀이 로그에 이 오류가 표시되는 경우 해상도 기반 출력 보호 정책을 검토하고 필요한 경우 컨텐츠를 다시 패키지해야 합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR:비디오 재생 값 {#section_7079501250C2487499639F92EC774525}

AVE의 Video Encoder 인터페이스는 `NATIVE_ERROR` 메타데이터 개체에서 이러한 비디오 재생 알림을 반환합니다.

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> NATIVE_ERROR_CODE 메타데이터 키 값 </th> 
   <th colname="col2" class="entry"> NATIVE_ERROR_NAME 메타데이터 키의 값 </th> 
   <th colname="col3" class="entry"> 설명 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> 기간이 종료되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 성공</span> </td> 
   <td colname="col3"> 작업이 성공했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 비동기 작업. 작업 요청이 수행되었습니다. 성공/실패 정보는 나중에 사용할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> 파일 끝(EOF) 조건으로 인해 작업을 수행할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> 런타임에 디코더가 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 하드웨어 디코더를 열지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND  </span> </td> 
   <td colname="col3"> 리소스를 찾을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR  </span> </td> 
   <td colname="col3"> 일반 오류입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR  </span> </td> 
   <td colname="col3"> 비디오 엔진을 복구할 수 없는 오류 조건입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE  </span> </td> 
   <td colname="col3"> 네트워크 오류입니다. 복구하려고 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE  </span> </td> 
   <td colname="col3"> 리소스의 크기를 확인할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED  </span> </td> 
   <td colname="col3"> 기능이 구현되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> OUT_OF_MEMORY  </span> </td> 
   <td colname="col3"> 메모리가 부족합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR  </span> </td> 
   <td colname="col3"> 미디어 파일을 구문 분석하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN  </span> </td> 
   <td colname="col3"> 리소스의 크기는 다르지만 알 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW  </span> </td> 
   <td colname="col3"> 언더플로우 조건. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG  </span> </td> 
   <td colname="col3"> 구성이 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION  </span> </td> 
   <td colname="col3"> 작업이 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT  </span> </td> 
   <td colname="col3"> 아직 초기화되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER  </span> </td> 
   <td colname="col3"> 매개 변수가 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19년 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> 작업이 허용되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20년 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> 작업은 일시 중지된 상태에만 허용됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 오디오 전용 파일에는 작업을 사용할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> 이전 검색 작업이 아직 진행 중입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED  </span> </td> 
   <td colname="col3"> 리소스를 지정하지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> 지정한 값이 범위를 벗어났습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> 검색 시간이 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 지정된 파일이 예상 구문을 따르지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> 필수 구성 요소를 만들 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> DRM 컨텍스트를 만들지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> 컨테이너 유형은 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> 검색에 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 지원되지 않는 코덱입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> 네트워크를 사용할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> 네트워크에서 데이터를 가져오는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 오버플로</span> </td> 
   <td colname="col3"> 오버플로입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 지원되지 않는 비디오 프로필입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> 보류 기간 또는 아직 로드되지 않은 기간에 작업을 시도했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 지정된 대체 기간이 잘못되었거나 스트림의 끝을 지나 확장됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> 잘못된 스레드에서 API를 호출할 수 없습니다. 대부분, Main 스레드에서만 호출해야 하는 API 요소의 경우. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> 조각 읽기 오류입니다. 장애 조치(failover)가 없습니다. 엔진은 다음 조각을 읽으려고 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> ABORTED</span> </td> 
   <td colname="col3"> 명시적 중단 또는 제거 호출로 작업이 중단되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> 이 버전의 HLS 미디어를 재생할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 실패할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP 다운로드 시간이 초과되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN  </span> </td> 
   <td colname="col3"> 사용자의 네트워크 연결이 끊겼습니다. 재생은 언제라도 중지될 수 있으며 연결을 사용할 수 있으면 다시 시작됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 스트림에 사용 가능한 비트 전송률 프로필이 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 매니페스트에 잘못된 서명이 있습니다. 매니페스트 서명 테스트에 실패했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 재생 목록을 로드할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> 삽입 API에 지정된 대체가 실패했습니다. 삽입에 성공했지만 대체가 되지 않았음을 의미합니다. 교체할 매니페스트를 타임라인에서 제거한 경우 교체가 실패할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_비대칭_PROFILE</span> </td> 
   <td colname="col3"> DRM이 비대칭 프로파일로 전환되고 있습니다. 모든 프로필은 지속 시간 단위로 정렬될 예정입니다. 그렇지 않으면 이 경고가 발생하고 재생 중에 이동할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 라이브 창은 앞으로 이동만 예상됩니다. 그렇지 않으면 이 경고가 발생하고 윈도우를 읽을 수 없습니다. 이로 인해 재생에 이동(또는 중지/긴 일시 중지)이 있을 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> 라이브 창이 현재 기간을 넘었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> HTTP 서버에서 보고한 컨텐츠 길이가 실제 미디어 크기와 일치하지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> 미디어 판독기가 setHoldAt API에 의해 설정된 시간에 도달했으므로 더 이상 읽을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD  </span> </td> 
   <td colname="col3">미디어 판독기가 라이브 창의 끝에 도달하여 세그먼트를 로드할 수 없습니다. 서버가 새 미디어를 라이브 창에 추가하면 세그먼트 로드가 다시 시작됩니다. 이 상태는 일반적으로 다음과 같은 경우에 도달합니다. 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48"><span class="codeph"> bufferTime</span>이(가) 너무 높음(라이브 윈도우 지속 시간과 같거나 더 높음). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">하나 이상의 삽입/지우기 API를 조합하여 추가한 것보다 더 많은 미디어를 대체합니다. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">다음 기간은 보류 중인 미디어 교체(InsertBy API 호출로 인해)가 있는 라이브 기간입니다 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEWING  </span> </td> 
   <td colname="col3"> 미디어의 오디오 및 비디오 인터리브가 제대로 수행되지 않습니다. 패키징 오류입니다. 차이가 2초를 초과하면 경고가 전달됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> Flash Player에서 HLS 재생이 활성화되지 않았습니다. AuthorizedFeatures.enableHLSPlayback을 참조하십시오. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 디코더가 디코딩할 수 없는 잘못된 샘플을 받았습니다. 이것은 보통 치명적인 오류는 아니지만 오디오/비디오에 문제가 있을 수 있음을 나타냅니다. 이 오류의 인스턴스가 너무 많으면 인코딩이 잘못되거나 파일이 잘못되었음을 나타냅니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 재생이 시작되면 삽입/바꾸기 범위에 읽기 헤드가 포함되지 않아야 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 포스트롤 삽입은 라이브 미디어에 사용할 수 없습니다. 그러나 서버가 미디어를 완료로 표시한 후에 허용됩니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> 절대로 일어나지 말아야 할 아주 드문 문제입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 스트림은 항상 H264 SPS/PPS를 AVCC에 배치하는 패키징 권장 사항을 따르지 않습니다. 검색/재생 문제가 표시될 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> 삽입 API에 지정된 대체는 부분적으로만 수행되었습니다. 이 문제는 타임라인 지속 시간에 걸쳐 replaceDuration 범위가 확장될 때 발생합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 변환 재생 목록을 로드하는 동안 오류가 발생했습니다. 이것은 AVE용이지 FlashPlayer용은 아닙니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> 작업이 아무 작업도 수행되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SWIGLED_ON_FAILURE</span> </td> 
   <td colname="col3"> 세그먼트를 재생할 수 없으며 실패 시 건너뜁니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> 호환되지 않는 렌더링 모드입니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> URL에 사용된 웹 프로토콜은 지원되지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> 미디어 파일을 구문 분석하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTED_CHANGED</span> </td> 
   <td colname="col3"> 매니페스트 파일이 예기치 않은 방식으로 변경되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 타임라인에서 분할 작업을 수행할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 타임라인에서 지우기 작업을 수행할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> 다음 조각을 가져오지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> 내부 데이터 구조에 타임라인이 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> 내부 데이터 구조에 리스너가 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 오디오를 시작할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> 내부 데이터 구조에 오디오 싱크가 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> 파일을 열 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> 파일에 쓸 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> 파일에서 읽을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> ID3 데이터를 구문 분석하는 동안 오류가 발생했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR  </span> </td> 
   <td colname="col3"> 보안 제한 때문에 콘텐츠를 로드하지 못했습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> 타임라인 기간이 너무 짧습니다. 라이브 스트림인 경우 버퍼링이 자주 발생할 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 스트림이 오디오 전용 스트림으로 전환되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 스트림이 비디오가 포함된 스트림으로 오디오 전용에서 전환되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND  </span> </td> 
   <td colname="col3"> 키를 찾을 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> 키가 잘못되었습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> 키 서버에서 키를 반환하지 않습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> 주 매니페스트 업데이트를 처리할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> 보고되지 않은 시간(PTS) 불연속성이 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> 일치하지 않는 오디오 및 비디오 연속성이 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3"><i>trick play</i> 모드에서 미디어를 재생하는 동안 오류가 발생했습니다. 트릭 재생 모드가 종료되고 스트림이 일시 중지됩니다. 일반 모드에서 미디어를 재생하려면 <span class="codeph"> Play()</span>를 호출합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> 그 선수는 라이브 윈도우를 벗어나서 앞으로 나아가 따라가야 한다. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR:암호화 값 {#section_39365E545CAC49B9A4D4678657BB2155}

Adobe 비디오 엔진의 암호화 모듈은 `NATIVE_ERROR` 메타데이터 개체에서 이러한 알림을 반환합니다.

| NATIVE_ERROR_CODE 메타데이터 키 값 | NATIVE_ERROR_NAME 메타데이터 키의 값 | 의미 |
|---|---|---|
| 300년 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 사용 중인 알고리즘은 지원되지 않습니다. |
| 301년 | `CRYPTO_ERROR_CORRUPTED_DATA` | 데이터가 손상되었습니다. |
| 302년 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 버퍼가 너무 작습니다. |
| 303년 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 인증서가 잘못되었습니다. |
| 304년 | `CRYPTO_ERROR_DIGEST_UPDATE` | 다이제스트 업데이트. |
| 305년 | `CRYPTO_ERROR_DIGEST_FINISH` | 다이제스트 완료 |
| 306년 | `CRYPTO_ERROR_BAD_PARAMETER` | 매개 변수가 잘못되었습니다. |
