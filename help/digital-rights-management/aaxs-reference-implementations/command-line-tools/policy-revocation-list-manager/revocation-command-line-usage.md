---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
exl-id: b9e51bab-7bef-459f-bb4d-13ccc4add37a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 명령줄 사용 {#command-line-usage}

해지 목록 관리자는 DVD의 \Reference Implementation\Command Line Tools 디렉터리에 있습니다. 도구를 실행하려면 다음 구문 중 하나를 사용합니다.

```
    java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` 해지 목록이 작성될 위치를 나타냅니다.
* `crlNumber` 는 CRL(인증서 해지 목록)의 음수가 아닌 버전 번호입니다. 이 숫자는 CRL이 업데이트될 때마다 증가해야 합니다.

다음 표에는 위의 구문에 표시된 명령줄 옵션에 대한 설명이 나와 있습니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 명령줄 옵션 </th> 
   <th colname="2" class="- topic/entry entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry ">구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 해지 목록 관리자가 다음을 찾습니다. <span class="filepath"> flashaccesstools.properties</span> 작업 디렉토리. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d 파일 이름</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">해지 목록에 대한 정보를 표시합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e 날짜</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(선택 사항) 해지 목록의 만료 날짜입니다. 형식 사용 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 또는 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:초</span> (예: 2009-01-31-14:30:00은 1월 31일 오후 2:30을 나타냅니다). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">기존 해지 목록에서 모든 항목을 추가합니다. 기존 파일은 하나만 지정할 수 있습니다. <p class="- topic/p ">이 기존 목록이 새 목록에 서명하는 데 사용 중인 자격 증명과 다른 자격 증명으로 서명된 경우 서명을 확인할 수 있도록 인증서 파일을 다음으로 지정하십시오. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 -o가 설정되지 않은 경우 오류가 반환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 확인하지 않고 덮어씁니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revotionDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">다음 사용자가 식별한 인증서 취소 <span class="codeph"> issuerName</span> 및 <span class="codeph"> 일련번호</span> 특정 날짜에. 다음 <span class="codeph"> issuerName</span> 은(는) 509 이름 형식을 따라야 합니다(예: <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). 일련 번호를 16진수 형식으로 지정합니다. 해지 날짜를 다음으로 지정: <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 또는 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:초</span>, 예: 2008-12-1 또는 2008-12-1-00:00:00 - 2008년 12월 1일 자정. 취소 날짜가 지정되지 않으면 현재 날짜가 사용됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>
