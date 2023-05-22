---
title: 개요
description: 개요
copied-description: true
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# DRM 정책 업데이트 목록 관리자 {#policy-update-list-manager}

Primetime DRM 정책 업데이트 목록 관리자 명령줄 도구 사용( [!DNL AdobePolicyUpdateListManager.jar])을 클릭하여 DRM 정책 업데이트 목록을 만들고 관리하며 정책이 업데이트되었는지 또는 취소되었는지 확인합니다.

정책 업데이트 목록 관리자 명령줄 도구를 실행하기 전에 *정책 업데이트 목록 관리자 및 해지 목록 관리자 속성* 섹션에 있는 마지막 항목이 될 필요가 없습니다.

>[!NOTE]
>
>명령줄에서 모든 정책 업데이트 목록 관리자 등록 정보를 지정할 수도 있습니다.

## 정책 업데이트 목록 관리자 명령줄 사용 {#policy-update-list-manager-command-line-usage}

**정책 업데이트 목록 만들기:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` DRM 정책 업데이트 목록이 작성된 파일의 이름을 나타냅니다.

**기존 정책 업데이트 목록 보기:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` 정책 업데이트 목록 파일의 이름입니다.

**표 4: 명령줄 옵션**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 이름과 위치를 지정합니다. </p> <p class="- topic/p ">이름이나 위치를 지정하지 않으면 DRM 정책 업데이트 목록 관리자에서 <span class="filepath"> flashaccesstools.properties </span> 를 입력합니다. </p> <p>참고: 명령줄에서 지정한 옵션이 구성 파일에서 지정한 옵션보다 우선합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d 파일 이름 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">DRM 정책 업데이트 목록에 대한 정보를 표시합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e 날짜 </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(선택 사항) DRM 정책 업데이트 목록의 만료 날짜입니다. </p> <p>형식 사용 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span> (예: 2009-01-31-14:30:00은 1월 31일 오후 2:30을 나타냅니다). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f 파일 이름 [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">기존 DRM 정책 업데이트 목록에서 모든 항목을 추가합니다. 기존 파일은 하나만 지정할 수 있습니다. </p> <p class="- topic/p ">기존 목록이 새 목록에 서명하는 데 사용되는 것과 다른 자격 증명으로 서명된 경우 해당 인증서 파일을 지정하여 서명을 확인해야 합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o </span> 가 설정되지 않은 경우 오류가 발생합니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 이미 있으면 확인하지 않고 덮어씁니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> 날짜 </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> 이유 URL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(선택 사항) 지정된 날짜의 DRM 정책 ID를 취소합니다. 선택 가능한 이유 코드, 이유 텍스트 및 이유 URL을 제공할 수 있습니다. 선택적 매개 변수에 대해 값이 제공되지 않음을 나타내려면 빈 문자열 ""을 지정해야 합니다. 다음에서 날짜를 지정할 수 있습니다. <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 또는 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:초 </span> 다음 형식으로 표시됩니다. 예: 2008-12-1 또는 2008-12-1-00:00:00은 2008년 12월 1일 자정을 나타냅니다.) 날짜를 지정하지 않으면 현재 날짜가 자동으로 적용됩니다. 따라서 이유 코드는 0보다 크거나 같아야 합니다. 여러 -r 옵션을 지정할 수도 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> 정책 파일 이름 </span> <span class="+ topic/ph pr-d/codeph codeph"> 날짜 </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> 이유 URL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">와 동일한 작업을 수행합니다. <span class="codeph"> -r </span> 옵션을 선택합니다. 그러나 지정된 파일에서 DRM 정책 식별자를 추출합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>지정된 이유 코드(선택 사항), 이유 텍스트(선택 사항) 및 이유 URL(선택 사항)을 사용하여 라이선스 요청의 일치하는 DRM 정책을 이 DRM 정책으로 바꿉니다. </p> <p>빈 문자열 ""은 선택적 매개 변수에 대한 값을 제공하지 않았음을 나타냅니다. </p> <p>이유 코드는 다음보다 크거나 같아야 합니다. <span class="codeph"> 0 </span>. 여러 을 지정할 수 있습니다 <span class="codeph"> -u </span> 옵션. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 구성 속성 {#configuration-properties}

다음 Primetime DRM 정책 업데이트 목록 관리자 속성은 암호와 함께 해지 목록(라이선스 서버 인증서)을 서명하기 위한 자격 증명이 포함된 PKCS12 파일을 지정합니다.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
