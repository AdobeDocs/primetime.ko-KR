---
seo-title: 명령줄 사용
title: 명령줄 사용
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 명령줄 사용 {#command-line-usage}

라이센스를 포함하려면 다음 구문을 사용하십시오.

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` 는 암호화된 FLV 또는 F4V 파일입니다.
* `destfile` 포함된 라이센스가 있는 암호화된 컨텐츠의 작성 위치를 지정합니다. 디렉토리를 지정하면 소스 파일과 동일한 파일 이름을 사용하여 파일이 이 디렉토리에 저장되지만 디렉토리가 소스 파일이 들어 있는 디렉토리는 아니어야 합니다.

다음 표에서는 이전에 언급한 구문과 함께 지정할 수 있는 명령줄 옵션에 대해 설명합니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 포함할 라이센스가 포함된 파일의 이름입니다. 여러 개의 라이선스를 임베드하기 위해 여러 <span class="codeph"> -l </span> 옵션을 지정할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 라이선스를 생성할 컨텐츠 메타데이터를 지정합니다. (라이선스를 생성하는 데 필요) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o를 </span> 설정하지 않으면 오류가 반환됩니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 확인하지 않고 덮어씁니다. </td> 
  </tr> 
 </tbody> 
</table>

