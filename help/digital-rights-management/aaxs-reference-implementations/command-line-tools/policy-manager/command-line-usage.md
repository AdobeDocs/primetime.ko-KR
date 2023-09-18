---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 명령줄 사용 {#command-line-usage}

정책 관리자를 사용하기 전에 요구 사항에 나열된 요구 사항을 충족하는지 확인하십시오.

정책 관리자는에 있습니다. [!DNL \Reference Implementation\Command Line Tools] dvd의 디렉토리. 도구를 실행하려면 다음 구문을 사용합니다.

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

다음 표에는 위의 구문에 표시된 명령줄 작업에 대한 설명이 나와 있습니다.

| 명령줄 동작 | 설명 |
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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 정책 관리자가 다음을 찾습니다. <span class="filepath"> flashaccesstools.properties </span> 작업 디렉토리. 명령줄에 지정된 옵션이 구성 파일에 있는 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 이미 있으면 확인하지 않고 덮어씁니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o </span> 가 설정되지 않은 경우 오류가 반환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책에 루트 라이선스가 있음을 나타냅니다. 업데이트가 허용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효하기 전날입니다. 다음으로 지정 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span>. 예: 2008-12-1 또는 2008-12-1-00:00:00 - 2008년 12월 1일 자정. 값은 다음 값보다 커야 합니다. <span class="codeph"> -s </span>, 있는 경우. 이 옵션은 와 함께 사용할 수 없습니다. <span class="codeph"> -r </span>. 정책을 업데이트할 때 종료 날짜를 제거하려면 <span class="codeph"> -e </span> 날짜를 지정하지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r분 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 정책으로 보호된 콘텐츠의 유효 기간(분)은 콘텐츠가 packager로 보호될 때부터 시작됩니다. 값은 음수가 아니어야 합니다. 이 옵션은 와 함께 사용할 수 없습니다. <span class="codeph"> -e </span>. 정책을 업데이트할 때 기간을 제거하려면 <span class="codeph"> -r </span> 분 수를 지정하지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스가 유효하게 되는 날짜입니다. 다음으로 지정 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span>. 예: 2008-12-1 또는 2008-12-1-00:00:00 - 2008년 12월 1일 자정. 값은 다음 값보다 작아야 합니다. <span class="codeph"> -e </span>, 있는 경우. 이 옵션은 와 함께 사용할 수 없습니다. <span class="codeph"> -r </span>. 정책을 업데이트할 때 시작 날짜를 제거하려면 <span class="codeph"> -s </span> 날짜를 지정하지 않았습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w분 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">재생 창(첫 번째 재생부터 컨텐츠가 표시될 수 있는 시간(분). 이 옵션이 지정되지 않았거나 <span class="codeph"> -w </span> 분 수를 지정하지 않고 를 사용합니다. 재생 시간 제한은 없습니다. 값은 음수가 아니어야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l분 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이선스 캐싱 기간(분)은 서버에서 라이선스를 발급한 후, 클라이언트의 라이선스 저장소에 라이선스가 캐시될 수 있는 시간입니다. 값은 음수가 아니어야 합니다. 지정 <span class="codeph"> -l 0 </span> 라이선스 캐싱이 허용되지 않음을 나타냅니다. 사용 <span class="codeph"> -l </span> 무제한 라이센스 캐싱에 대한 시간(분)을 지정하지 않아도 됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -date 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">라이센스 캐싱 종료 일자(서버에서 라이센스를 발행한 후, 클라이언트의 라이센스 저장소에 라이센스가 캐시될 수 없는 일자). 다음으로 지정 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>또는<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span>. 예: 2008-12-1 또는 2008-12-1-00:00:00 - 2008년 12월 1일 자정. 사용 <span class="codeph"> -l </span> 무제한 라이센스 캐싱에 대한 시간(분)을 지정하지 않아도 됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">인증 네임스페이스입니다. 지정하면 지정된 기관에서 발급한 사용자 이름과 암호로 클라이언트를 인증해야 합니다. 이 옵션은 와 함께 사용할 수 없습니다. <span class="codeph"> -x </span>. 업데이트에 허용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">익명 액세스를 허용합니다. 이 옵션은 와 함께 사용할 수 없습니다. <span class="codeph"> -authNS </span>. 업데이트에 허용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> 분 </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 컨텐츠 재생이 허용되는 AIR 애플리케이션 허용 목록. 이 정책으로 보호된 콘텐츠에 액세스할 수 있는 게시자, 애플리케이션 및 버전을 제한하려면 이 옵션을 사용하십시오. </p> <p class="- topic/p ">If <i class="+ topic/ph hi-d/i ">appId</i> 은(는) 지정되지 않았습니다. 게시자용 모든 응용 프로그램입니다. <i class="+ topic/ph hi-d/i ">pubId</i> 허용됩니다. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">분</i> 및 <i class="+ topic/ph hi-d/i ">max</i> 버전 번호는 선택 사항입니다. </p> <p class="- topic/p ">복수 <span class="codeph"> -air </span> 여러 애플리케이션을 허용하도록 옵션을 지정할 수 있습니다. AIR 또는 SWF 애플리케이션을 지정하지 않으면 모든 애플리케이션이 이 콘텐츠에 액세스할 수 있습니다. 업데이트하는 동안 나머지 인수 없이 -air를 사용하여 목록에서 모든 항목을 제거합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist 이름 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 클라이언트의 보호된 콘텐츠 액세스가 제한됨. 값은 다음 형식의 쉼표로 구분된 name:value 쌍으로 구성됩니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue </span> </p> <p class="- topic/p ">예를 들어, <span class="codeph"> os=Win,release=2.0.1 </span>. 업데이트하는 동안 다음을 사용하십시오. <span class="codeph"> -drmBlacklist </span> 목록에서 모든 항목을 제거할 수 있도록 나머지 인수를 추가합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 클라이언트가 보호된 콘텐츠에 액세스하려면 지정된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | 필수 | 재생 없음(_R) | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">아날로그 출력 보호 제한. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | 필수 | 재생 없음(_R) </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">디지털 출력 보호 제한. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist 이름 </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> 값 </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> 쌍 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">응용 프로그램 실행 시간이 보호된 콘텐츠에 액세스하지 못하도록 제한되었습니다. 값은 다음 형식의 쉼표로 구분된 name:value 쌍으로 구성됩니다. </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | 응용 프로그램 | release= stringValue </span> </p> <p class="- topic/p ">예를 들어, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. 업데이트하는 동안 다음을 사용하십시오. <span class="codeph"> -runtimeBlacklist </span> 목록에서 모든 항목을 제거할 수 있도록 나머지 인수를 추가합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">응용 프로그램 런타임에 보호된 콘텐츠에 액세스하려면 지정된 최소 보안 수준이 있어야 함을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf 파일= swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">보호된 컨텐츠 재생이 허용되는 SWF 애플리케이션 허용 목록. 여러 개의 응용 프로그램을 허용하도록 여러 개의 -swf 옵션을 지정할 수 있습니다. AIR 또는 SWF 애플리케이션을 지정하지 않으면 모든 애플리케이션이 이 콘텐츠에 액세스할 수 있습니다. 업데이트하는 동안 나머지 인수 없이 -swf를 사용하여 목록에서 모든 항목을 제거합니다. 해시 값으로 SWF을 식별하려면 해시를 계산할 SWF 파일과 SWF 확인을 완료할 수 있는 최대 시간(초)을 지정합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책에 추가할 사용자 지정 키/값을 지정합니다. 복수 <span class="codeph"> -k </span> 옵션을 지정할 수 있습니다. 업데이트하는 동안 다음을 사용하십시오. <span class="codeph"> -k </span> 모든 속성을 제거할 수 있도록 나머지 인수를 추가합니다. 이 데이터의 해석 또는 처리는 전적으로 Adobe 액세스 라이선스 서버의 구현에 달려 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">각 클라이언트에 대해 생성된 라이선스에 표시되는 사용자 지정 속성을 추가합니다. 복수 <span class="codeph"> -p </span> 여러 속성을 추가하도록 옵션을 지정할 수 있습니다. 업데이트하는 동안 다음을 사용하십시오. <span class="codeph"> -p </span> 모든 속성을 제거할 수 있도록 나머지 인수를 추가합니다. 이 데이터의 해석 또는 처리는 전적으로 클라이언트 애플리케이션의 구현에 달려 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
