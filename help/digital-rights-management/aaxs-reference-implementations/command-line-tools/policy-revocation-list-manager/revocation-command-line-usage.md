---
seo-title: 명령줄 사용
title: 명령줄 사용
uuid: 273e9d3b-efeb-46fa-a4b1-f13247b4e498
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 명령줄 사용 {#command-line-usage}

해지 목록 관리자는 DVD의 \Reference Implementation\Command Line Tools 디렉토리에 있습니다. 도구를 실행하려면 다음 구문 중 하나를 사용합니다.

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
* `crlNumber` 는 CRL(인증서 해지 목록)의 음수가 아닌 버전 번호입니다. 이 번호는 CRL이 업데이트될 때마다 증가합니다.

다음 표에는 위의 구문에 나와 있는 명령줄 옵션에 대한 설명이 나와 있습니다.

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
   <td colname="2" class="- topic/entry ">구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 해지 목록 관리자에서 작업 디렉토리에서 flashaccesstools. <span class="filepath"> properties</span> 를 찾습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d 파일 이름</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">해지 목록에 대한 정보를 표시합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e 날짜</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(선택 사항) 해지 목록의 만료 날짜. yyyy-mm-dd <span class="+ topic/ph pr-d/codeph codeph">또는</span> yyyy-mm-dd-h24:min:sec:sec <span class="+ topic/ph pr-d/codeph codeph"></span> 형식을 사용합니다(예: 2009-01-31-14:30:00은 1월 31일을 오후 2:30으로 나타냅니다). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">기존 해지 목록에서 모든 항목을 추가합니다. 기존 파일은 하나만 지정할 수 있습니다. <p class="- topic/p ">이 기존 목록이 새 목록에 서명하는 데 사용되는 인증서와 다른 자격 증명으로 서명된 경우 다음 인증서 파일을 지정하여 서명을 확인할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 이미 있고 -o가 설정되어 있지 않으면 오류가 반환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 확인하지 않고 덮어씁니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">지정된 날짜에 발급자 <span class="codeph"> 이름</span> 및 <span class="codeph"> 시리얼</span> 번호로 식별된 인증서를 해지합니다. 발급자 <span class="codeph"> 이름은</span> 509 이름 형식을 따라야 합니다(예: <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). 일련 번호를 16진수 형식으로 지정합니다. 해지 날짜를 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 또는 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>(예: 2008-12-1-00:00 - 2008년 12월 1일 자정)으로 지정합니다. 해지 날짜가 지정되지 않으면 현재 날짜가 사용됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

