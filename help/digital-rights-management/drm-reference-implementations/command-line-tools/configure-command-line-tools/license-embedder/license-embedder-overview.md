---
seo-title: 개요
title: 개요
uuid: 5487d1d3-7eb8-410d-a4b1-cde3e94c00a1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# DRM 라이선스 임베드 {#license-embedder}

Media Packager [!DNL AdobeLicenseEmbedder.jar] 가 보호하는 콘텐츠에 사전 생성된 라이선스를 임베드하는 데 사용합니다.

## 라이선스 임베드 명령줄 사용 {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` 는 암호화된 파일을 나타냅니다.
* `destfile` 포함된 라이센스가 있는 암호화된 컨텐츠가 저장되는 파일의 이름을 지정합니다.

   디렉토리를 지정하면 파일이 대상 디렉토리에 저장됩니다. 소스 파일의 이름도 대상 디렉토리에 저장된 파일의 이름이 됩니다.

다음 표에서는 지정할 수 있는 명령줄 옵션에 대해 설명합니다.

**표 7:옵션**

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
   <td colname="2" class="- topic/entry "> 포함할 라이센스가 포함된 파일의 이름입니다. 여러 개의 <span class="codeph"> -l </span> 옵션을 지정하여 여러 개의 라이선스를 포함할 수 있습니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 라이선스를 생성할 수 있는 컨텐츠 메타데이터를 지정합니다. 이 옵션은 라이센스를 생성하는 데 필요합니다. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일을 덮어쓸지 묻지 않습니다. 대상 파일이 이미 있고 <span class="codeph"> -o </span> 가 적용되지 않은 경우 오류가 발생합니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 대상 파일이 이미 있으면 메시지가 표시되지 않고 덮어쓸 수 있습니다. </td> 
  </tr> 
 </tbody> 
</table>
