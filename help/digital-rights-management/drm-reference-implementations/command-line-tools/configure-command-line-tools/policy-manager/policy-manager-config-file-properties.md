---
description: 'null'
keywords: hard stop
seo-description: 'null'
seo-title: 구성 속성
title: 구성 속성
uuid: 216921d1-a9c1-4650-9dce-c025836986e5
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# 구성 속성 {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>포함된 속성 이름 `.n`의 경우 이 `n` 는 속성의 각 인스턴스에 대해 1로 시작하고 증가되는 정수를 나타냅니다. 예: `policy.license.customProp.n`.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 속성/명령줄 옵션 </th> 
   <th colname="2" class="- topic/entry entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">policyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 사람이 읽을 수 있는 DRM 정책 이름입니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">부울</i> </p> </td> 
   <td colname="2" class="- topic/entry ">다음 조건이 적용됩니다. 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">true인 경우 iOS로의 키 전달을 위해 HTTPS 키 서버가 필요합니다. </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">지정하지 않으면 기본값은 false입니다. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">부울</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 탈옥을 지원하는 장치의 경우, true이면 탈옥이 감지될 때 재생을 허용하지 않습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM 정책의 중요도를 설정합니다. 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">true인 경우 서버는 기본 동작을 나타내는 DRM 정책의 모든 부분을 이해해야 합니다. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">false인 경우 서버는 인식할 수 없는 DRM 정책 속성을 무시할 수 있습니다. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asynamication.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">고급 라이센스 체인에 대한 루트 암호화 키를 암호화하는 데 공개 키를 사용하는 라이센스 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 서버 인증서</a>. 이 속성은 인증서만 포함하는 파일을 지정합니다. <p>참고:  PEM 또는 DER 형식 모두 지원됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">루트 키</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>고급 라이센스 체인의 루트 암호화 키를 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 지정합니다</a>. 키를 지정하지 않고 고급 라이센스 체인이 활성화되어 있으면 임의 키가 자동으로 생성됩니다. </p> <p>키는 16바이트입니다. 16진수 값으로 지정됩니다. 16진수 값 사이의 공백은 선택 사항입니다. 업데이트의 경우 명령줄 옵션을 사용할 수 없으며 속성은 무시됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">도메인 등록이 필요한 경우 <i>url</i> 은 도메인 서버의 URL을 지정합니다. 업데이트의 경우 명령줄 옵션을 사용할 수 없으며 속성은 무시됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">익명 도메인 등록이 허용되는지 여부를 지정합니다. 속성을 true로 설정하거나 익명 액세스를 허용하도록 이 명령줄 옵션을 포함합니다. <p>참고: 이 옵션은 <span class="codeph"> -domainAuthNS와 함께 사용할 수 없습니다</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">네임스페이스</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>도메인 등록을 위한 인증 네임스페이스입니다. 지정된 경우 클라이언트는 지정된 기관이 발행한 사용자 이름과 암호로 인증해야 합니다. </p> <p>업데이트의 경우 명령줄 옵션을 사용할 수 없으며 속성은 무시됩니다. </p> <p>참고: 이 옵션은 <span class="codeph"> -domainAnon과 함께 사용할 수 없습니다</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">아날로그 출력 보호 제한 및 다음 값이 지원됩니다. 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> 필수</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>보호된 콘텐츠에 대한 액세스가 제한된 DRM 클라이언트 이 옵션은 사용할 수 없는(차단 목록) DRM 모듈 버전의 목록을 지정합니다. </p> <p>값은 다음 형식으로 쉼표로 구분된 <span class="codeph"> 이름=값</span> 쌍으로 구성됩니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">추가 이름/값 쌍은 쉼표로 구분해야 합니다. 예: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>응용 프로그램 런타임은 보호된 콘텐츠에 액세스할 수 없습니다. 이 옵션은 사용할 수 없는(차단 목록) 런타임 모듈 버전의 목록을 지정합니다. </p> <p>값은 다음 형식의 쉼표로 구분된 <span class="codeph"> 이름=값</span> 쌍으로 구성됩니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">추가 이름/값 쌍은 쉼표로 구분해야 합니다. 예: <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하는 데 필요한 장치 기능을 지정합니다. 값은 다음 형식으로 쉼표로 구분된 <span class="codeph"> 이름=값</span> 쌍으로 구성됩니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">예를 들어 nonUserAccessibleBus=false,hardwareRootOfTrust=true <span class="codeph"> 입니다</span>. </p> <p>업데이트하는 동안 장치 기능 제한을 제거하는 나머지 인수 없이 <span class="codeph"> -devCapabilitiesV1</span> 을 적용해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트가 동기화 메시지를 서버에 보내는 데 필요한 빈도를 지정합니다. </p> <p>속성이 설정되지 않은 경우 클라이언트가 DRM 정책으로 보호된 내용을 재생할 때 동기화 메시지를 보내지 않습니다. 값은 다음 형식의 쉼표로 구분된 <span class="codeph"> 이름=값</span> 쌍으로 구성됩니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">다음 목록은 옵션에 대한 추가 정보를 제공합니다. 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(필수) <span class="codeph"> start</span> 는 클라이언트가 마지막 동기화 이후 지정된 분 내에 서버와 동기화를 시작해야 함을 지정합니다. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(선택 사항) force <span class="codeph"></span> 는 클라이언트가 재생 중에 동기화 메시지를 강제 적용해야 하는 확률(0-100)입니다. </li> 
     </ul>업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -sync</span> 를 사용하여 동기화 요구 사항을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">이 DRM 정책에 루트 라이센스가 있는지 여부를 나타냅니다. <p>자세한 내용은 고급 라이센스 체인 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 을 참조하십시오</a>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">컨텐츠가 유효한 날짜입니다. 다음 형식 중 하나를 적용할 수 있습니다. 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> <p>예를 들어 <span class="codeph"> 2009-01-31</span> 은 1월 31일 오전 12:00을 의미합니다. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> <p>예를 들어 <span class="codeph"> 2009-01-31-14:30:00은 1월 31일 오후 2:30을 의미합니다</span> . </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">콘텐츠가 유효하지 않게 되기 전의 날짜입니다. </p> <p>참고: policy.expiration.endDate <span class="codeph"> 및</span> policy.expiration.duration을 동시에 지정할 수 <span class="codeph"></span> 없습니다. </p> <p>예를 들어 2009-01-31-14:30:00은 컨텐츠가 1월 31일 오후 2:30에 만료됨을 의미합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">컨텐츠가 유효하지 않은 시간(분)입니다. 시간은 컨텐츠를 패키지할 때 시작됩니다. </p> <p>참고: policy.expiration.endDate <span class="codeph"> 및</span> policy.expiration.duration을 동시에 지정할 수 <span class="codeph"></span> 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트에서 라이선스를 캐싱할 수 있는 시간(분)입니다. 이 속성을 0으로 설정하여 라이선스 캐시를 방지할 수 있습니다. 값은 0 이상이어야 합니다. </p> <p>참고: policy.licenseCaching.duration <span class="codeph"> 및</span> policy.licenseCaching.endDate를 동시에 지정할 수 <span class="codeph"></span> 없습니다. </p> <p class="- topic/p ">이 DRM 정책 설정은 디스크의 라이선스 캐시에만 적용되며 메모리 캐시된 라이선스 기간은 제어하지 않습니다. 지속 시간이 0인 DRM 정책을 지정하지 않아도 라이센스는 메모리에 캐시될 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">더 이상 라이선스를 캐싱할 수 없는 날짜입니다. </p> <p>참고: policy.licenseCaching.duration <span class="codeph"> 및</span> policy.licenseCaching.endDate를 동시에 지정할 수 <span class="codeph"></span> 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">익명 라이선스 획득이 허용되는지 여부를 나타냅니다. 기본값은 false로 설정되며 <span class="codeph"></span>, 즉 사용자 이름과 암호가 필요합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">사용자 이름과 암호가 필요한 경우 이 속성은 사용자 이름에 대한 선택적 이름 한정자를 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이센스 취득 동안 서버에서 사용할 사용자 지정 이름/값 쌍입니다. 다음 형식을 적용하여 속성을 지정할 수 있습니다. <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">재생 창을 분 단위로 지정합니다. 이 값은 보호된 콘텐츠를 처음 재생한 후 라이선스가 유효한 기간을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">출력 보호 제한 - 다음 값 중 하나여야 합니다. 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> 필수</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">나열할 수 있도록 허용해야 하는 OTA(대기) 연결 유형을 지정합니다. 유효한 연결 유형은 다음과 같습니다. 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> 에어플레이</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> 해상도 기반 제약 조건을 정의하는 구성 파일을 지정합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 모듈에서 보호된 콘텐츠에 액세스할 수 있도록 허용하는 최소 보안 수준을 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하려면 응용 프로그램 런타임 모듈에 최소 보안 수준이 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash 애플리케이션이 아닌 허용 목록(Adobe AIR, iOS, Android 등) 보호된 콘텐츠를 재생할 수 있습니다. 속성은 다음 형식을 사용해야 합니다. <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 SWF 애플리케이션의 허용 목록 속성은 다음 형식을 사용해야 합니다. </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> is the SWF file that is used to compute the hash, and <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> is the maximum time in second that is allowed to download and verify the SWF to complete. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">사용자에게 라이센스가 발급될 때 라이센스에 포함해야 하는 사용자 정의 이름/값 쌍. 다음 형식을 지정해야 합니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">여러 사용자 지정 속성에 대해 이 옵션을 여러 번 정의할 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
