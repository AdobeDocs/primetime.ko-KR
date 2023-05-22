---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
exl-id: 241849bb-e818-420e-98b4-c12e306b17b2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 명령줄 사용 {#command-line-usage}

라이센스를 생성하려면 다음 구문을 사용합니다.

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` 는 Adobe 액세스 DRM 메타데이터를 포함하는 .metadata 파일입니다. 이 파일은 보호된 콘텐츠에서 `-d -m` Media Packager 옵션.

이전에 생성된 라이센스를 표시하려면 다음 구문을 사용합니다.

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 는 라이센스 생성기에서 생성한 Adobe 액세스 라이센스가 포함된 파일입니다.

다음 표에서는 앞에서 언급한 구문과 함께 지정할 수 있는 명령줄 옵션에 대해 설명합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry "> 구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 라이센스 생성기가 작업 디렉토리에서 flashaccesstools.properties를 찾습니다. 명령줄에 지정된 옵션이 구성 파일에 있는 옵션보다 우선합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 이미 생성된 라이선스에 대한 정보를 표시합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 리프 라이선스를 생성하고 출력을 지정된 파일에 기록합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m 메타데이터-파일 이름</span> </td> 
   <td colname="2" class="- topic/entry "> 라이센스를 생성할 컨텐츠 메타데이터를 지정합니다. (라이선스 생성에 필요) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o</span> 가 설정되지 않은 경우 오류가 반환됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 확인하지 않고 덮어씁니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> 메타데이터에 여러 정책이 포함된 경우 라이센스를 생성하는 데 사용할 정책(1부터 시작) 수를 지정합니다. 지정하지 않으면 첫 번째 정책이 사용됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">지정된 수신자에 대한 라이선스를 생성합니다. 디바이스 또는 도메인 인증서를 사용할 수 있습니다. 복수 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>여러 수신자에 대한 라이선스를 만들도록 옵션을 지정할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 루트 라이선스를 생성하고 출력을 지정된 파일에 기록합니다. </td> 
  </tr> 
 </tbody> 
</table>
