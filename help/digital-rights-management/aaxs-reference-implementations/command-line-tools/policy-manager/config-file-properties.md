---
seo-title: 구성 파일 속성
title: 구성 파일 속성
uuid: aec5fee7-4d77-4299-8d85-3e9042b2bbd1
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# 구성 파일 속성 {#configuration-file-properties}

구성 파일은 다음 속성을 지정합니다. 포함된 속성 이름 `n`의 경우 속성 `n` 의 각 인스턴스에 대해 1로 시작하는 정수를 나타냅니다.

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
   <td colname="2" class="- topic/entry "> 사람이 읽을 수 있는 정책 이름. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">부울</i> </p> </td> 
   <td colname="2" class="- topic/entry "> true인 경우 iOS로의 키 전달을 위해 HTTPS 키 서버가 필요합니다. 지정하지 않으면 기본값은 false입니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">부울</i> </p> </td> 
   <td colname="2" class="- topic/entry "> true인 경우, 탈옥을 지원하는 장치의 경우 탈옥이 감지된 경우 재생을 허용하지 않습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 정책 중요성 설정 true이면 서버가 정책의 모든 부분(기본 동작)을 이해해야 합니다. false일 경우, 서버는 이해할 수 없는 정책 속성을 무시할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asynamication.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">공개 키를 사용하여 고급 라이센스 체인의 루트 암호화 키를 암호화하는 데 사용되는 라이센스 서버 인증서 <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> </a>이 속성은 인증서 전용(PEM 또는 DER 형식 중 하나)을 포함하는 파일을 지정합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">루트 키</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 고급 라이센스 체인에 대한 루트 암호화 키를 지정합니다. 키를 지정하지 않고 고급 라이센스 체인이 활성화되면 임의 키가 생성됩니다. 키는 길이 16바이트입니다. 16진수 값으로 지정됩니다. 16진수 값 사이의 공백은 선택 사항입니다. 업데이트의 경우 명령줄 옵션이 허용되지 않으며 속성은 무시됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 도메인 등록이 필요한 경우 도메인 서버의 URL입니다. 업데이트의 경우 명령줄 옵션이 허용되지 않으며 속성은 무시됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> 익명 도메인 등록이 허용되는지 여부를 지정합니다. 속성을 true로 설정하거나 이 명령줄 옵션을 포함하여 익명 액세스를 허용합니다. 이 옵션은 -domainAuthNS와 함께 사용할 수 없습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">네임스페이스</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 도메인 등록을 위한 인증 네임스페이스입니다. 지정된 경우 클라이언트는 지정된 기관이 발행한 사용자 이름과 암호로 인증해야 합니다. 업데이트의 경우 명령줄 옵션이 허용되지 않으며 속성은 무시됩니다. 이 옵션은 -domainAnon과 함께 사용할 수 없습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">아날로그 출력 보호 제한. 다음 값이 지원됩니다. 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 필수</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">DRM 클라이언트는 보호된 콘텐츠에 액세스할 수 없도록 제한됩니다. 이 옵션은 사용할 수 없는 DRM 모듈(블록 목록) 버전의 목록을 지정합니다. 값은 다음 형식의 쉼표로 구분된 이름=값 쌍으로 구성됩니다. <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">추가 이름/값 쌍은 쉼표로 구분해야 합니다. 예: <span class="codeph"> os=Win,릴리스=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry ">응용 프로그램 런타임은 보호된 콘텐츠에 액세스할 수 없도록 제한됩니다. 이 옵션은 사용할 수 없는 런타임 모듈 버전 목록을 지정합니다(블록 목록). 값은 다음 형식의 쉼표로 구분된 이름=값 쌍으로 구성됩니다. <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">추가 이름/값 쌍은 쉼표로 구분해야 합니다. 예: <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하는 데 필요한 장치 기능을 지정합니다. 값은 다음 형식의 쉼표로 구분된 이름=값 쌍으로 구성됩니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">예를 들어 nonUserAccessibleBus=false,hardwareRootOfTrust=true <span class="codeph"> 입니다</span>. 업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -devCapabilitiesV1</span> 키를 사용하여 장치 기능 제한을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트가 동기화 메시지를 서버에 보내는 데 필요한 빈도를 지정합니다. 설정하지 않으면 클라이언트는 이 정책으로 보호된 내용을 재생할 때 동기화 메시지를 전송하지 않습니다. 값은 다음 형식의 쉼표로 구분된 <span class="codeph"> 이름=value</span> 쌍으로 구성됩니다. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> 시작</span> (필수) - 시작 간격은 클라이언트가 마지막 동기화 이후 이 시간(분) 동안 서버와 동기화를 시작할 것을 지정합니다. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span> (선택 사항) - 강제 동기화 가능성은 클라이언트가 재생 중에 동기화 메시지를 강제 적용할 확률(0-100)입니다. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> (선택 사항) - 하드 정지 간격은 동기화할 수 없는 경우 클라이언트가 재생되지 못할 때의 시간(분)입니다. 설정된 경우 시작 간격보다 커야 합니다. </li> 
     </ul>업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -sync</span> 를 사용하여 동기화 요구 사항을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">이 정책에 루트 라이센스가 있는지 여부를 나타냅니다(컨텐츠 보호를 위해 <i class="+ topic/ph hi-d/i ">Adobe 액세스</i> 사용 <i class="+ topic/ph hi-d/i ">에서 향상된 라이센스 체인</i>참조). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">컨텐츠가 유효한 날짜입니다. yyyy- <span class="+ topic/ph pr-d/codeph codeph">mm-dd</span> 형식 사용(예: <span class="codeph"> 2009-01-31은 1월 31일을 오전 12:00으로 표시) 또는</span> yyyy-mm-dd-h24:min:sec <span class="+ topic/ph pr-d/codeph codeph">(예:</span> <span class="codeph"></span> 2009-01-314:3 0:00는 1월 31일 오후 2시 30분)을 나타냅니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">컨텐츠가 유효한 날짜입니다. policy.expiration.endDate <span class="codeph"></span> 및 policy.expiration.duration 모두 동시에 지정할 수 없습니다. yyyy-mm-dd <span class="+ topic/ph pr-d/codeph codeph">또는</span> yyyy-mm-dd-h24:min:sec <span class="+ topic/ph pr-d/codeph codeph"></span> 형식을 사용하십시오(예: 2009-01-31-14:30:00은 1월 31일을 오후 2:30으로 나타냅니다). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">컨텐츠가 패키지될 때부터 시작하여 컨텐츠가 유효한 시간(분)입니다. policy.expiration.endDate <span class="codeph"> 및</span> policy.expiration.duration <span class="codeph"></span> 모두 동시에 지정할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트에 라이센스가 캐시될 수 있는 시간(분) 라이선스 캐시를 허용하지 않으려면 이 속성을 0으로 설정합니다. 값은 0 이상이어야 합니다. policy.licenseCaching.duration <span class="codeph"> 및</span> policy.licenseCaching.endDate <span class="codeph"></span> 모두 동시에 사용할 수 없습니다. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">참고</b>: 이 정책 설정은 디스크의 라이선스 캐시에만 적용됩니다. 메모리 캐시된 라이선스 지속 시간은 제어하지 않습니다. 정책으로 지정된 기간이 0인 경우에도 라이선스는 메모리에 캐시될 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스를 캐시할 수 없는 날짜입니다. policy.licenseCaching.duration <span class="codeph"> 및</span> policy.licenseCaching.endDate <span class="codeph"></span> 모두 동시에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">익명 라이선스 획득이 허용되는지 여부를 나타냅니다. 지정하지 않을 경우 기본값은 "false"입니다(사용자 이름/암호 인증 필요). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">사용자 이름/암호 인증이 필요한 경우 이 속성은 사용자 이름에 대한 선택적 이름 한정자를 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이센스 취득 동안 서버에서 사용할 사용자 지정 이름/값 쌍입니다. 속성을 지정하려면 다음 형식을 사용하십시오. <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생하는 데 처음 사용된 이후 라이선스의 유효 기간인 재생 창(분)을 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">출력 보호 제한. 값은 다음 중 하나여야 합니다. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, 필수, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하려면 DRM 모듈에 지정된 최소 보안 수준 이상이 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하려면 응용 프로그램 런타임 모듈에 지정된 최소 보안 수준 이상이 있어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 Adobe AIR 또는 iOS 애플리케이션의 허용 목록입니다. 속성은 다음 형식을 사용해야 합니다. <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 SWF 응용 프로그램의 허용 목록입니다. 다음 형식을 사용하십시오. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> 또는 file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>,time=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> swf_file <i class="+ topic/ph hi-d/i ">은 SWF의 다운로드 및 확인을 완료할 수 있도록 허용하는 최대 시간(초)인 해시 값을 계산하는 SWF</i> <i class="+ topic/ph hi-d/i "></i> 파일입니다. max_time_to verifySWF는 SWF의 다운로드 및 확인을 위한 최대 시간(초)입니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">사용자에게 발급된 라이선스에 포함할 사용자 정의 이름/값 쌍. 다음 형식을 사용하십시오. </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">이 옵션은 여러 사용자 지정 속성에 대해 여러 번 정의할 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

