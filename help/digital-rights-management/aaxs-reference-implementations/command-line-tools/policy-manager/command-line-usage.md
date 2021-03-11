---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---


# 명령줄 사용 {#command-line-usage}

정책 관리자를 사용하기 전에 요구 사항에 나와 있는 요구 사항을 충족해야 합니다.

정책 관리자가 DVD의 [!DNL \Reference Implementation\Command Line Tools] 디렉토리에 있습니다. 도구를 실행하려면 다음 구문을 사용합니다.

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

다음 표에는 위의 구문에 나와 있는 명령줄 작업에 대한 설명이 나와 있습니다.

| 명령줄 작업 | 설명 |
|---|---|
| `new` | 새 정책을 만듭니다. |
| `detail` | 기존 정책을 설명합니다. |
| `update` | 기존 정책을 업데이트합니다. |

다음 표에서는 위의 구문과 함께 지정할 수 있는 명령줄 옵션에 대해 설명합니다.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 정책 관리자가 작업 디렉토리에서 <span class="filepath"> flashaccesstools.properties </span>을 찾습니다. 명령줄에 지정된 옵션이 구성 파일에 있는 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 이미 있으면 묻지 않고 덮어씁니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o </span>이(가) 설정되어 있지 않으면 오류가 반환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책에 루트 라이센스가 있음을 나타냅니다. 업데이트는 허용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효한 날짜입니다. <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>로 지정합니다. 예를 들어 2008년 12월 1일 자정을 위해 2008-12-1 또는 2008-12-1-00:00:00이 표시됩니다. 값은 <span class="codeph"> -s </span> 값보다 커야 합니다(있는 경우). 이 옵션은 <span class="codeph"> -r </span>과 함께 사용할 수 없습니다. 정책을 업데이트할 때 종료 날짜를 제거하려면 날짜를 지정하지 않고 <span class="codeph"> -e </span> 를 사용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r 분  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 정책으로 보호된 콘텐트가 패키지로 보호되는 시간부터 유효한 기간(분)입니다. 값은 음수가 아니어야 합니다. 이 옵션은 <span class="codeph"> -e </span>와 함께 사용할 수 없습니다. 정책을 업데이트할 때 기간을 제거하려면 시간(분)을 지정하지 않고 <span class="codeph"> -r </span>을 사용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효한 날짜입니다. <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>로 지정합니다. 예를 들어 2008년 12월 1일 자정을 위해 2008-12-1 또는 2008-12-1-00:00:00이 표시됩니다. 값은 <span class="codeph"> -e </span> 값보다 작아야 합니다(있는 경우). 이 옵션은 <span class="codeph"> -r </span>과 함께 사용할 수 없습니다. 정책을 업데이트할 때 시작 날짜를 제거하려면 날짜를 지정하지 않고 <span class="codeph"> -s </span>를 사용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w 분  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">재생 창(첫 번째 재생부터 내용을 볼 수 있는 시간(분)입니다. 이 옵션이 지정되지 않았거나 시간(분)을 지정하지 않고 <span class="codeph"> -w </span>를 사용하는 경우 재생 창 제한이 없습니다. 값은 음수가 아니어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l 분  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 기간(분)입니다. 이 기간은 서버에서 라이선스를 발급한 후 클라이언트의 라이선스 저장소에서 라이선스를 캐싱할 수 있는 시간입니다. 값은 음수가 아니어야 합니다. 라이선스 캐싱이 허용되지 않음을 나타내려면 <span class="codeph"> -l 0 </span>을 지정합니다. 무제한 라이센스 캐싱에 대한 시간(분)을 지정하지 않고 <span class="codeph"> -l </span>을 사용합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -date 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 종료 날짜(서버에서 라이선스를 발급한 후 클라이언트의 라이선스 저장소에 라이센스가 캐시되지 않을 수 있는 날짜). <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span></i> <i class="+ topic/ph hi-d/i "> <i class="+ topic/ph hi-d/i "> <span class="+ topic/ph pr-d/codeph codeph"> </i> yyyy-mm-dd-h24:min:sec </span>으로 지정합니다. 예를 들어 2008년 12월 1일 자정을 위해 2008-12-1 또는 2008-12-1-00:00:00이 표시됩니다. 무제한 라이센스 캐싱에 대한 시간(분)을 지정하지 않고 <span class="codeph"> -l </span>을 사용합니다. </i></p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">인증 네임스페이스입니다. 지정된 경우 클라이언트는 지정된 기관에서 발급한 사용자 이름과 암호로 인증되어야 합니다. 이 옵션은 <span class="codeph"> -x </span>과 함께 사용할 수 없습니다. 업데이트는 허용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">익명 액세스 허용 이 옵션은 <span class="codeph"> -authNS </span>과 함께 사용할 수 없습니다. 업데이트는 허용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 AIR 응용 프로그램의 허용 목록. 이 정책으로 보호된 콘텐츠에 액세스할 수 있는 게시자, 응용 프로그램 및 버전을 제한하려면 이 정책을 사용합니다. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">appId</i>가 지정되지 않은 경우 게시자 <i class="+ topic/ph hi-d/i ">pubId</i>에 대한 모든 응용 프로그램이 허용됩니다. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">minand </i> maxversion  <i class="+ topic/ph hi-d/i "></i> 번호는 선택 사항입니다. </p> <p class="- topic/p ">여러 응용 프로그램을 허용하도록 <span class="codeph"> -air </span> 옵션을 여러 개 지정할 수 있습니다. AIR 또는 SWF 응용 프로그램을 지정하지 않은 경우 모든 응용 프로그램에서 이 내용에 액세스할 수 있습니다. 업데이트하는 동안 나머지 인수 없이 -air를 사용하여 목록에서 모든 항목을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist 이름  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 클라이언트는 보호된 콘텐츠에 대한 액세스를 제한합니다. 이 값은 쉼표 구분 이름:다음 형식의 값 쌍으로 구성됩니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">예: <span class="codeph"> os=Win,release=2.0.1 </span>. 업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -drmBlacklist </span> 를 사용하여 목록에서 모든 항목을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하려면 DRM 클라이언트가 지정된 최소 보안 수준을 가져야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | 필수 | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">아날로그 출력 보호 제약 조건 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | 필수 | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">디지털 출력 보호 제약 조건 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist 이름  </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">응용 프로그램 런타임은 보호된 콘텐츠에 액세스할 수 없도록 제한됩니다. 이 값은 쉼표 구분 이름:다음 형식의 값 쌍으로 구성됩니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | 응용 프로그램 | release= stringValue  </span> </p> <p class="- topic/p ">예: <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. 업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -runtimeBlacklist </span>을(를) 사용하여 목록에서 모든 항목을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 콘텐츠에 액세스하려면 응용 프로그램 런타임에 지정된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf 파일= swf_file  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 내용을 재생할 수 있는 SWF 응용 프로그램의 허용 목록. 여러 응용 프로그램을 허용하도록 여러 -swf 옵션을 지정할 수 있습니다. AIR 또는 SWF 응용 프로그램을 지정하지 않은 경우 모든 응용 프로그램에서 이 내용에 액세스할 수 있습니다. 업데이트하는 동안 나머지 인수 없이 -swf를 사용하여 목록에서 모든 항목을 제거합니다. SWF를 해시 값으로 식별하려면 해시를 계산할 SWF 파일과 SWF 확인을 완료할 수 있는 최대 시간(초)을 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= 값  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책에 추가할 사용자 지정 키/값을 지정합니다. <span class="codeph"> -k </span> 옵션을 여러 개 지정할 수 있습니다. 업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -k </span>을 사용하여 모든 속성을 제거합니다. 이 데이터를 해석하거나 처리하는 것은 Adobe 액세스 라이선스 서버의 구현에 전적으로 적용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p 이름= 값  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">각 클라이언트에 대해 생성된 라이선스에 표시되는 사용자 지정 속성을 추가합니다. 여러 속성을 추가하려면 여러 <span class="codeph"> -p </span> 옵션을 지정할 수 있습니다. 업데이트하는 동안 나머지 인수 없이 <span class="codeph"> -p </span>을 사용하여 모든 속성을 제거합니다. 이 데이터의 해석 또는 처리는 클라이언트 응용 프로그램의 구현에 전적으로 달려 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

