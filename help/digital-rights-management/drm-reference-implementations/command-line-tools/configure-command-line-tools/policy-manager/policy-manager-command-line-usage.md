---
title: 정책 관리자 명령줄 사용
description: 정책 관리자 명령줄 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# 정책 관리자 명령줄 사용 {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**표 1:명령**

| 명령 | 설명 |
|---|---|
| `new` | 새 DRM 정책 만들기 |
| `detail` | 기존 DRM 정책 설명 |
| `update` | 기존 DRM 정책 업데이트 |

**표 2:옵션**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p> <p class="- topic/p ">이름이나 위치를 지정하지 않으면 DRM 정책 관리자가 현재 작업 디렉토리에서 <span class="filepath"> flashaccesstools.properties </span>을 검색합니다. </p> <p>참고: 명령줄에서 지정하는 옵션은 구성 파일에서 지정하는 옵션에 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 있으면 메시지가 표시되지 않고 파일을 덮어쓸 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 있고 <span class="codeph"> -o </span>이(가) 설정되어 있지 않으면 오류가 발생합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책에 루트 라이센스가 있음을 나타냅니다. </p> <p class="- topic/p ">이 옵션은 업데이트에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효한 날짜입니다. </p> <p><span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> 형식으로 날짜를 지정할 수 있습니다. 예를 들어 2008년 12월 1일 자정을 위해 2008-12-1 또는 2008-12-1-00:00:00이 표시됩니다. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">이 값은 <span class="codeph"> -s </span> 값보다 커야 합니다(있는 경우). </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">이 옵션은 <span class="codeph"> -r </span>과 함께 적용할 수 없습니다. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">DRM 정책을 업데이트할 때 종료 날짜를 제거하려면 날짜를 지정하지 않고 <span class="codeph"> -e </span> 을 적용합니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r 분  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠가 유효한 기간(분)입니다. </p> <p class="- topic/p ">콘텐츠가 패키지로 보호되면 DRM 정책이 유효합니다. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">값은 음수가 아니어야 합니다. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">이 옵션은 <span class="codeph"> -e </span>와 함께 적용할 수 없습니다. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">DRM 정책을 업데이트할 때 지속 시간을 제거하거나 삭제하려면 분을 지정하지 않고 <span class="codeph"> -r </span> 을 적용합니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효한 날짜입니다. </p> <p><span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> 형식으로 날짜를 지정할 수 있습니다. 예를 들어 2008년 12월 1일 자정에 대해 <span class="codeph"> 2008-12-1 </span> 또는 <span class="codeph"> 2008-12-1-00:00:00 </span> 등이 있습니다. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">값은 <span class="codeph"> -e </span> 값보다 작아야 합니다(있는 경우). </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">이 옵션은 <span class="codeph"> -r </span>과 함께 적용할 수 없습니다. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">DRM 정책을 업데이트할 때 시작 날짜를 제거하거나 삭제하려면 날짜를 지정하지 않고 <span class="codeph"> -s </span> 을 사용합니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,ENABLEHS|disableHS]]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">재생 창 - 첫 번째 재생에서 내용을 볼 수 있는 시간(분)입니다. </p> <p>지정되지 않거나 시간(분)을 지정하지 않고 <span class="codeph"> -w </span>를 사용하는 경우 재생 창 제한이 없습니다. 값은 음수가 아니어야 합니다. </p> <p>선택 사항인 <span class="codeph"> enableHS </span> 또는 <span class="codeph"> disableHS </span> 플래그는 하드 중지를 활성화할지 또는 비활성화할지를 나타냅니다. 이 플래그는 암호 해독 컨텍스트가 재생 창 끝(활성화)에 제거되었는지(비활성화) 여부를 나타냅니다. </p> <p>예를 들어 컨텐츠를 60분 동안만 볼 수 있고 하드 스루가 필요하도록 지정하려면: 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>참고: <i>하드 중지</i>는 현재 Flash Player, Android 및 iOS에서 지원되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l 분  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 기간은 서버에서 라이선스를 발급한 후 클라이언트의 라이선스 저장소에서 라이선스를 캐싱할 수 있는 시간(분)입니다. 값은 음수가 아니어야 합니다. </p> <p><span class="codeph"> -l 0 </span>을(를) 지정하여 라이선스 캐싱이 허용되지 않음을 나타낼 수 있습니다. 무제한 라이센스 캐싱의 경우 <span class="codeph"> -l </span>을(를) 분 없이 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -date 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 종료 날짜입니다. </p> <p class="- topic/p ">Primetime DRM 서버가 라이선스를 발행한 후 클라이언트가 클라이언트의 라이선스 스토어에서 라이선스를 캐싱할 수 있는 최종 날짜를 나타냅니다. </p> <p>날짜를 다음 형식으로 지정할 수 있습니다. 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd  </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec  </span> </li> 
     </ul>예를 들어 2008년 12월 1일 자정에 대해 <span class="codeph"> 2008-12-1 </span> 또는 <span class="codeph"> 2008-12-1-00:00:00 </span> 등이 있습니다. 무제한 라이센스 캐싱에 대한 시간을 분 단위로 지정하지 않고 <span class="codeph"> -l </span>을(를) 적용해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">인증 네임스페이스입니다. </p> <p class="- topic/p ">이 옵션을 적용하면 클라이언트는 지정된 기관이 발행한 사용자 이름과 암호를 입력해야 합니다. </p> <p>이 옵션은 <span class="codeph"> -x </span>와 함께 적용할 수 없습니다. </p> <p>이 옵션은 업데이트에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">익명 액세스 허용 </p> <p class="- topic/p ">이 옵션은 <span class="codeph"> -authNS </span>과 함께 적용할 수 없습니다. </p> <p class="- topic/p ">이 옵션은 업데이트에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 AIR 애플리케이션의 허용 목록. </p> <p class="- topic/p ">이 옵션을 적용하여 이 DRM 정책으로 보호된 콘텐츠에 액세스할 수 있는 게시자, 응용 프로그램 및 버전을 제한할 수 있습니다. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">appId</i>를 지정하지 않으면 게시자 <i class="+ topic/ph hi-d/i ">pubId</i>에 대한 모든 응용 프로그램이 허용됩니다. </p> <p>참고: <i class="+ topic/ph hi-d/i ">min</i> 및 <i class="+ topic/ph hi-d/i ">max</i> 버전 번호는 선택 사항입니다. </p> <p class="- topic/p ">여러 응용 프로그램을 허용하려면 여러 <span class="codeph"> -air </span> 옵션을 지정할 수 있습니다. AIR 또는 SWF 응용 프로그램을 지정하지 않으면 모든 응용 프로그램이 이 내용에 액세스할 수 있습니다. 업데이트하는 동안 목록에서 모든 항목을 제거하거나 삭제하려면 나머지 인수 없이 <span class="codeph"> -air </span> 을 적용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist 이름  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 대한 액세스가 제한된 DRM 클라이언트. </p> <p class="- topic/p ">이 값은 다음 형식의 쉼표로 구분된 이름:값 쌍을 지원합니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">예: <span class="codeph"> os=Win,release=2.0.1 </span>. 업데이트하는 동안 목록에서 모든 항목을 제거하려면 나머지 인수 없이 <span class="codeph"> -drmBlacklist </span>을(를) 적용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 대한 액세스를 받으려면 DRM 클라이언트에 할당된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | 필수 | NO_PLAYBACK | REQUIRED_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">아날로그 출력 보호 제한 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | 필수 | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">디지털 출력 보호 제한 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist 이름  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 대한 액세스가 제한된 응용 프로그램 런타임입니다. </p> <p class="- topic/p ">값은 다음 형식의 쉼표 구분 이름:값 쌍을 지원합니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | 응용 프로그램 | release= stringValue  </span> </p> <p class="- topic/p ">예: <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. 업데이트하는 동안 목록에서 모든 항목을 제거하려면 나머지 인수 없이 <span class="codeph"> -runtimeBlacklist </span>을(를) 적용하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하려면 응용 프로그램 런타임에 지정된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf 파일= swf_file  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 SWF 응용 프로그램의 허용 목록. </p> <p class="- topic/p ">여러 개의 <span class="codeph"> -swf </span> 옵션을 지정하여 여러 응용 프로그램을 허용할 수 있습니다. AIR 또는 SWF 응용 프로그램을 지정하지 않으면 모든 응용 프로그램이 이 내용에 액세스할 수 있습니다. </p> <p>업데이트하는 동안 목록에서 모든 항목을 제거하려면 나머지 인수 없이 <span class="codeph"> -swf </span> 를 적용합니다. 해시 값으로 SWF를 식별하려면 해시를 계산할 SWF 파일과 SWF 확인을 완료할 수 있는 최대 시간(초)을 지정해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= 값  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책에 추가할 사용자 지정 키/값을 지정합니다. </p> <p class="- topic/p ">여러 <span class="codeph"> -k </span> 옵션을 지정할 수 있습니다. 모든 속성을 제거하려면 나머지 인수 없이 <span class="codeph"> -k </span> 을 적용할 수 있습니다. 데이터에 대한 해석 또는 처리는 Primetime DRM 라이선스 서버에서 관리합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p 이름= 값  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">각 클라이언트에 대해 생성된 라이선스에 나타나는 사용자 지정 속성을 추가합니다. </p> <p class="- topic/p ">여러 <span class="codeph"> -p </span> 옵션을 지정하여 여러 속성을 추가할 수 있습니다. 모든 속성을 제거하려면 나머지 인수 없이 <span class="codeph"> -p </span> 을 적용해야 합니다. 이 데이터의 해석 또는 처리는 클라이언트 응용 프로그램의 구현에 의해 관리됩니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA 화이트리스트=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> OTA(대기) 출력 보호 제한. <span class="codeph"> 화이트리스트 </span> 필드는 허용 목록에 대한 연결 유형을 지정하고 &lt;connection types&gt; 형식은 <span class="codeph"> [type(,type)*] </span>입니다. 여기서 유형은 다음 중 하나일 수 있습니다.MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution  &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>지정된 파일에 정의된 해상도 기반 출력 보호 제한. </p> <p>이 파일의 인코딩은 JSON입니다. 서식에 대한 문법은 <i>해상도 기반 출력 보호 정보</i>에서 찾을 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

**예**

고유한 구성 속성 파일을 사용하여 컨텐트에 대한 익명 액세스를 허용하는 정책을 만들려면:

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
