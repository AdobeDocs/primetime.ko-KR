---
title: 정책 관리자 명령줄 사용
description: 정책 관리자 명령줄 사용
copied-description: true
exl-id: 888be282-7eaa-4101-b4b1-4f8df99a967a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# 정책 관리자 명령줄 사용 {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**표 1: 명령**

| 명령 | 설명 |
|---|---|
| `new` | 새 DRM 정책 생성 |
| `detail` | 기존 DRM 정책을 설명합니다. |
| `update` | 기존 DRM 정책 업데이트 |

**표 2: 옵션**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p> <p class="- topic/p ">이름이나 위치를 지정하지 않으면 DRM 정책 관리자가 다음을 검색합니다. <span class="filepath"> flashaccesstools.properties </span> 를 입력합니다. </p> <p>참고: 명령줄에서 지정한 옵션이 구성 파일에서 지정한 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 있으면 메시지가 표시되지 않고 파일을 덮어쓸 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 있고 <span class="codeph"> -o </span> 가 설정되지 않은 경우 오류가 발생합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책에 루트 라이센스가 있음을 나타냅니다. </p> <p class="- topic/p ">이 옵션은 업데이트에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이센스가 유효화되기 전날입니다. </p> <p>다음에서 날짜를 지정할 수 있습니다. <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span> 포맷. 예: 2008-12-1 또는 2008-12-1-00:00:00 - 2008년 12월 1일 자정. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">값은 다음 값보다 커야 합니다. <span class="codeph"> -s </span> 있는 경우. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">에는 이 옵션을 적용할 수 없습니다. <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">DRM 정책을 업데이트할 때 종료 날짜를 제거하려면 을 적용합니다 <span class="codeph"> -e </span> 날짜를 지정하지 않았습니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r분 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠가 유효한 기간(분)입니다. </p> <p class="- topic/p ">콘텐츠가 패키지로 보호되면 DRM 정책이 유효해집니다. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">값은 음수가 아니어야 합니다. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">이 옵션은 과 함께 적용할 수 없습니다. <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">DRM 정책을 업데이트할 때 지속 시간을 제거하거나 삭제하려면 를 적용합니다 <span class="codeph"> -r </span> 을(를) 지정하지 않았습니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효하게 되는 날짜. </p> <p>다음에서 날짜를 지정할 수 있습니다. <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span> 포맷. 예를 들어, <span class="codeph"> 2008-12-1 </span> 또는 <span class="codeph"> 2008-12-1-00:00:00 </span> 2008년 12월 1일 자정에. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">값은 다음 값보다 작아야 합니다. <span class="codeph"> -e </span>, 있는 경우. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">이 옵션은 과 함께 적용할 수 없습니다. <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">DRM 정책을 업데이트할 때 시작 날짜를 제거하거나 삭제하려면 <span class="codeph"> -s </span> 날짜를 지정하지 않았습니다. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">재생 창: 첫 번째 재생에서 컨텐츠를 볼 수 있는 시간(분)입니다. </p> <p>지정되지 않은 경우 또는 <span class="codeph"> -w </span> 분 수를 지정하지 않고 를 사용합니다. 재생 시간 제한은 없습니다. 값은 음수가 아니어야 합니다. </p> <p>선택 사항 <span class="codeph"> enableHS </span> 또는 <span class="codeph"> disableHS </span> 하드 정지를 활성화할지 비활성화할지 여부를 플래그로 표시합니다. 이 플래그는 해독 컨텍스트가 재생 창의 끝에서 제거되는지(활성화됨) 또는 제거되지 않는지(비활성화됨) 여부를 나타냅니다. </p> <p>예를 들어 콘텐츠를 60분 동안만 볼 수 있도록 지정하려면 하드 중지를 수행해야 합니다. 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>참고:  <i>하드 스톱</i> 은 현재 Flash Player, Android 및 iOS에서 지원되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l분 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 기간은 서버에서 라이선스를 발급한 후, 클라이언트의 라이선스 저장소에 라이선스를 캐시할 수 있는 시간(분)입니다. 값은 음수가 아니어야 합니다. </p> <p>다음을 지정할 수 있습니다. <span class="codeph"> -l 0 </span> 라이센스 캐싱이 허용되지 않음을 나타냅니다. 무제한 라이선스 캐싱의 경우 다음을 지정하십시오. <span class="codeph"> -l </span> 아무 분도 없이. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -date 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 종료 날짜입니다. </p> <p class="- topic/p ">이는 Primetime DRM 서버가 라이선스를 발급한 후 클라이언트가 클라이언트의 라이선스 저장소에 라이선스를 캐시할 수 있는 최종 날짜를 나타냅니다. </p> <p>다음과 같은 형식으로 날짜를 지정할 수 있습니다. 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span> </li> 
     </ul>예를 들어, <span class="codeph"> 2008-12-1 </span> 또는 <span class="codeph"> 2008-12-1-00:00:00 </span> 2008년 12월 1일 자정에. 지원해야 합니다. <span class="codeph"> -l </span> 무제한 라이선스 캐싱에 대한 시간(분)을 지정하지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">인증 네임스페이스입니다. </p> <p class="- topic/p ">이 옵션을 적용하는 경우 클라이언트는 지정된 기관에서 발급한 사용자 이름과 암호를 입력해야 합니다. </p> <p>이 옵션은 과 함께 적용할 수 없습니다. <span class="codeph"> -x </span>. </p> <p>이 옵션은 업데이트에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">익명 액세스를 허용합니다. </p> <p class="- topic/p ">이 옵션은 과 함께 적용할 수 없습니다. <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">이 옵션은 업데이트에 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 분 </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠를 재생할 수 있는 AIR 애플리케이션 허용 목록. </p> <p class="- topic/p ">이 옵션을 적용하여 이 DRM 정책으로 보호되는 콘텐츠에 액세스할 수 있는 게시자, 애플리케이션 및 버전을 제한할 수 있습니다. </p> <p class="- topic/p ">을 지정하지 않은 경우 <i class="+ topic/ph hi-d/i ">appId</i>, 게시자용 응용 프로그램 모두 <i class="+ topic/ph hi-d/i ">pubId</i> 허용됩니다. </p> <p>참고:  <i class="+ topic/ph hi-d/i ">분</i> 및 <i class="+ topic/ph hi-d/i ">max</i> 버전 번호는 선택 사항입니다. </p> <p class="- topic/p ">여러 을 지정할 수 있습니다 <span class="codeph"> -air </span> 여러 응용 프로그램을 허용하는 옵션입니다. AIR 또는 SWF 애플리케이션을 지정하지 않으면 모든 애플리케이션이 이 콘텐츠에 액세스할 수 있습니다. 업데이트하는 동안 목록에서 모든 항목을 제거하거나 삭제하려면 를 적용합니다 <span class="codeph"> -air </span> 나머지 인수 없이 . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist 이름 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 대한 액세스가 제한되는 DRM 클라이언트. </p> <p class="- topic/p ">이 값은 다음 형식으로 쉼표로 구분된 name:value 쌍을 지원합니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue </span> </p> <p class="- topic/p ">예를 들어, <span class="codeph"> os=Win,release=2.0.1 </span>. 업데이트하는 동안 목록에서 모든 항목을 제거하려면 을 적용합니다 <span class="codeph"> -drmBlacklist </span> 나머지 인수 없이 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 클라이언트가 보호된 콘텐츠에 액세스하려면 할당된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | 필수 | 재생 없음(_R) | 필수_ACP | 필수_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">아날로그 출력 보호 제한 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | 필수 | 재생 없음(_R) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">디지털 출력 보호 제한 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist 이름 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 대한 액세스가 제한되는 애플리케이션 실행 시간. </p> <p class="- topic/p ">값은 다음 형식의 쉼표로 구분된 name:value 쌍을 지원합니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | 응용 프로그램 | release= stringValue </span> </p> <p class="- topic/p ">예를 들어, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. 업데이트하는 동안 목록에서 모든 항목을 제거하려면 을 적용합니다 <span class="codeph"> -runtimeBlacklist </span> 나머지 인수 없이 . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">응용 프로그램 실행 시간에 보호된 콘텐츠에 액세스하려면 지정된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf 파일= swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 컨텐츠 재생이 허용되는 SWF 애플리케이션 허용 목록. </p> <p class="- topic/p ">여러 을 지정할 수 있습니다 <span class="codeph"> -swf </span> 여러 응용 프로그램을 허용하는 옵션입니다. AIR 또는 SWF 애플리케이션을 지정하지 않으면 모든 애플리케이션이 이 콘텐츠에 액세스할 수 있습니다. </p> <p>업데이트하는 동안 목록에서 모든 항목을 제거하려면 을 적용합니다 <span class="codeph"> -swf </span> 나머지 인수 없이 . 해시 값으로 SWF을 식별하려면 해시를 계산할 SWF 파일과 SWF 확인을 완료할 수 있는 최대 시간(초)을 지정해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책에 추가할 사용자 지정 키/값을 지정합니다. </p> <p class="- topic/p ">여러 을 지정할 수 있습니다 <span class="codeph"> -k </span> 옵션. 업데이트 중에 다음을 적용할 수 있습니다. <span class="codeph"> -k </span> 모든 속성을 제거하려면 나머지 인수를 사용하십시오. 데이터의 해석 또는 처리는 Primetime DRM 라이센스 서버에 의해 관리됩니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">각 클라이언트에 대해 생성된 라이선스에 표시되는 사용자 지정 속성을 추가합니다. </p> <p class="- topic/p ">여러 을 지정할 수 있습니다 <span class="codeph"> -p </span> 여러 속성을 추가하는 옵션입니다. 업데이트하는 동안 를 적용해야 합니다. <span class="codeph"> -p </span> 모든 속성을 제거하려면 나머지 인수를 사용하십시오. 이 데이터의 해석 또는 처리는 클라이언트 애플리케이션의 구현에 의해 관리된다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA 허용 목록=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> OTA(Over the air) 출력 보호 제한 다음 <span class="codeph"> 화이트 리스트 </span> 필드는 허용 목록 할 연결 유형과 형식을 지정합니다. &lt;connection types=""&gt; 은(는) <span class="codeph"> [type(,type)*] </span>여기서 type은 MIRACAST, AIRPLAY, WIDI, DLNA 중 하나일 수 있습니다. </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>지정된 파일에 정의된 해상도 기반 출력 보호 제한. </p> <p>이 파일의 인코딩은 JSON입니다. 서식에 대한 문법은에서 찾을 수 있습니다. <i>해상도 기반 출력 보호 정보</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**예**

고유한 구성 속성 파일을 사용하여 콘텐츠에 대한 익명 액세스를 허용하는 정책을 만들려면 다음 작업을 수행하십시오.

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
