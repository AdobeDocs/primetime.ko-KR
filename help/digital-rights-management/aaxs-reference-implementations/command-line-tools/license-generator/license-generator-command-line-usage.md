---
title: 명령줄 사용
description: 명령줄 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# 명령줄 사용 {#command-line-usage}

라이센스를 생성하려면 다음 구문을 사용하십시오.

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` 는 Adobe 액세스 DRM 메타데이터가 포함된 .metadata 파일입니다. 이 파일은 Media Packager의 `-d -m` 옵션을 사용하여 보호된 콘텐츠에서 가져올 수 있습니다.

이전에 생성된 라이센스를 표시하려면 다음 구문을 사용하십시오.

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 는 라이센스 생성기에 의해 생성된 Adobe 액세스 라이센스가 포함된 파일입니다.

다음 표에서는 이전에 설명한 구문과 함께 지정할 수 있는 명령줄 옵션에 대해 설명합니다.

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
   <td colname="2" class="- topic/entry "> 구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 라이센스 생성기에서 작업 디렉토리에서 flashaccess.properties를 찾습니다. 명령줄에 지정된 옵션이 구성 파일에 있는 옵션보다 우선합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 이미 생성된 라이선스에 대한 정보를 표시합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 리프 라이선스를 생성하여 지정된 파일에 출력을 쓸 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 라이선스를 생성할 콘텐츠 메타데이터를 지정합니다. (라이선스를 생성하는 데 필요) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o</span>이(가) 설정되어 있지 않으면 오류가 반환됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 묻지 않고 덮어씁니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> 메타데이터에 여러 정책이 포함되어 있는 경우 라이선스를 생성하는 데 사용할 정책(1부터 시작)의 수를 지정합니다. 지정하지 않으면 첫 번째 정책이 사용됩니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">지정된 수신자에 대한 라이선스를 생성합니다. 장치 또는 도메인 인증서를 사용할 수 있습니다. 여러 수신자에 대한 라이센스를 만들기 위해 여러 개의 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>옵션을 지정할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 루트 라이선스를 생성하고 지정된 파일에 출력을 기록합니다. </td> 
  </tr> 
 </tbody> 
</table>

