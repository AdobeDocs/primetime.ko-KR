---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# 명령줄 사용 {#command-line-usage}

정책 업데이트 목록 관리자는 DVD의 \Reference Implementation\Command Line Tools 디렉토리에 있습니다. 정책 업데이트 목록을 만들려면 다음 구문을 사용하십시오.

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 정책 업데이트 목록을 작성할 위치를 나타냅니다.

기존 정책 업데이트 목록을 보려면 다음 구문을 사용하십시오.

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

다음 표에는 위의 구문에 나와 있는 명령줄 옵션에 대한 설명이 나와 있습니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 정책 업데이트 목록 관리자가 작업 디렉토리에서 <span class="filepath"> flashaccesstools.properties </span>을 찾습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d 파일 이름  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책 업데이트 목록에 대한 정보를 표시합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e 날짜  </span> </td> 
   <td colname="2" class="- topic/entry "> (선택 사항) 정책 업데이트 목록의 만료 날짜입니다. <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> 형식을 사용합니다(예: 2009-01-31-14:30:00은 1월 31일을 오후 2:30으로 나타냅니다). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f 파일 이름 [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">기존 정책 업데이트 목록에서 모든 항목을 추가합니다. 기존 파일은 하나만 지정할 수 있습니다. </p> <p class="- topic/p ">이 기존 목록이 새 목록에 서명하는 데 사용하는 자격 증명과 다른 자격 증명으로 서명된 경우 해당 인증서 파일을 지정하여 서명을 확인할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o </span>이(가) 설정되어 있지 않으면 오류가 반환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 이미 있으면 묻지 않고 덮어씁니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID  </span> <span class="+ topic/ph pr-d/codeph codeph"> date  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode  </span>"  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "  <span class="+ topic/ph pr-d/codeph codeph">   </span>reasonURL" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(선택 사항) 지정된 날짜에 정책 ID를 취소합니다. 선택 가능한 이유 코드, 이유 텍스트 및 이유 URL도 제공됩니다. 선택적 매개 변수에 대해 값이 제공되지 않음을 나타내려면 빈 문자열 ""을 지정합니다. 날짜를 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>(예: 2008년 12월 1일 자정에는 2008-12-1 또는 2008-12-1-00:00:00)로 지정합니다. 날짜를 지정하지 않으면 현재 날짜가 사용됩니다. 이유 코드는 0보다 크거나 같아야 합니다. 다중 -r 옵션을 지정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> 날짜 </span> reasonCode <span class="+ topic/ph pr-d/codeph codeph">" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>"</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">-r 플래그와 동일한 작업을 수행하지만 지정된 파일에서 정책 식별자를 추출합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>지정된 이유 코드(선택 사항), 이유 텍스트(선택 사항) 및 이유 URL(선택 사항)을 사용하여 라이센스 요청의 모든 일치 정책을 이 정책으로 바꿉니다. </p> <p>선택적 매개 변수에 대해 값이 제공되지 않음을 나타내려면 빈 문자열 ""을 지정합니다. </p> <p>원인 코드는 <span class="codeph"> 0 </span>보다 크거나 같아야 합니다. <span class="codeph"> -u </span> 옵션을 여러 개 지정할 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

