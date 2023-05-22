---
title: DRM 해지 목록 관리자
description: DRM 해지 목록 관리자
copied-description: true
exl-id: 5b17d195-30ca-4005-b710-83a6f77779a2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# DRM 해지 목록 관리자 {#policy-revocation-list-manager}

Primetime DRM 해지 목록 관리자 명령줄 도구 사용( [!DNL AdobeRevocationListManager.jar])를 클릭하여 해지 목록을 만들고 관리하며, 정책이 해지되었는지 확인합니다.

실행하기 전에 [!DNL AdobeRevocationListManager.jar]에서 속성을 설정해야 합니다. *정책 업데이트 목록 관리자 및 해지 목록 관리자 속성* 섹션에 있는 마지막 항목이 될 필요가 없습니다.

>[!NOTE]
>
>명령줄에서 모든 해지 목록 관리자 속성을 지정할 수도 있습니다.

## 해지 목록 관리자 명령줄 사용 {#revocation-list-manager-command-line-usage}

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

* `destfile` 해지 목록 속성이 저장되는 파일의 이름을 지정합니다.
* `crlNumber` CRL(인증서 해지 목록)의 음수가 아닌 버전 번호를 나타냅니다. CRL이 업데이트될 때마다 이 숫자를 증가시켜야 합니다.

**표 5: 명령줄 옵션**

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
   <td colname="2" class="- topic/entry "><p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p><p class="- topic/p ">이름 또는 위치를 지정하지 않으면 DRM 해지 목록 관리자가 다음을 검색합니다. <span class="filepath"> flashaccesstools.properties</span> 를 입력합니다. </p><p>참고: 명령줄에서 지정한 옵션이 구성 파일에서 지정한 옵션보다 우선합니다. </p>구성 파일의 위치를 지정합니다. 이 옵션을 적용하지 않으면 해지 목록 관리자가 다음을 검색합니다. <span class="filepath"> flashaccesstools.properties</span> 작업 디렉토리. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d 파일 이름</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">해지 목록에 대한 정보를 표시합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e 날짜</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(선택 사항) 해지 목록의 만료 날짜입니다. 다음 형식 중 하나를 사용합니다. 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:초</span> </li> 
     </ul>예: 2009-01-31-14:30:00은 1월 31일 오후 2시 30분을 나타냅니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>기존 해지 목록에서 모든 항목을 추가합니다. 기존 파일은 하나만 지정할 수 있습니다. </p> <p class="- topic/p ">기존 목록이 새 목록에 서명하는 데 사용한 자격 증명이 아닌 다른 자격 증명으로 서명된 경우 서명 확인 옆에 인증서 파일을 지정해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o</span> 가 설정되지 않은 경우 오류가 발생합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 메시지가 표시되지 않고 덮어쓸 수 있습니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revotionDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이(가) 식별한 인증서 취소 <span class="codeph"> issuerName</span> 및 <span class="codeph"> 일련번호</span> 지정한 날짜에. 다음 <span class="codeph"> issuerName</span> 은(는) 509 이름 형식을 사용해야 합니다. 예를 들어, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>일련 번호를 16진수 형식으로 지정해야 합니다. 또한 다음 형식 중 하나로 해지 날짜를 지정해야 합니다. 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:초</span> </li> 
     </ul>예: 2008-12-1 또는 2008-12-1-00:00:00 - 2008년 12월 1일 자정. 취소 날짜를 지정하지 않으면 현재 날짜가 자동으로 적용됩니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 구성 속성 {#configuration-properties}

해지 목록에 서명하려면 자격 증명을 적용해야 합니다. 다음 해지 목록 관리자 속성은 인증서 암호와 함께 해지 목록(라이선스 서버 인증서)에 서명하기 위한 자격 증명이 포함된 PKCS12 파일을 지정합니다.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
