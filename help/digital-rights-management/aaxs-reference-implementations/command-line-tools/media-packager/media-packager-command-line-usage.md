---
seo-title: 명령줄 사용
title: 명령줄 사용
uuid: 5f24f18d-09ef-400a-9404-50a9fcf4316d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# 명령줄 사용 {#command-line-usage}

Media Packager를 사용하기 전에 요구 사항에 나열된 요구 사항을 충족하고 구성 파일에 필요한 정보가 포함되어 있는지 확인하십시오(Adobe 액세스 참조 구현 사용 *의 구성 파일 참조*).

Media Packager는 DVD의 [!DNL \Reference Implementation\Command Line tools] 디렉토리에 있습니다. 단일 파일을 암호화하려면 다음 구문을 사용하십시오.

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` 는 암호화할 파일입니다.
* `dest` 암호화된 내용을 쓸 위치를 지정합니다. 디렉토리를 지정하면 암호화된 파일이 소스 파일과 동일한 파일 이름을 사용하여 이 폴더에 저장되지만 해당 디렉토리가 소스 파일을 포함하는 디렉토리가 아니어야 합니다.

동일한 키(다중 비트 전송률 지원을 위해)로 여러 파일을 암호화하려면 다음 구문을 사용하십시오.

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` 는 암호화할 파일을 나타내는 일련의 공백으로 구분된 소스 항목입니다.
* `dest-directory` 암호화된 내용을 쓸 위치를 지정합니다. 암호화된 파일은 소스 파일과 동일한 파일 이름을 사용하여 이 폴더에 저장되지만 해당 디렉토리가 소스 파일이 포함된 디렉토리가 아니어야 합니다.

암호화된 파일에 대한 정보를 보려면 다음 구문을 사용하십시오.

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` 는 암호화된 파일입니다.

메타데이터 파일에 대한 정보를 보려면 다음 구문을 사용하십시오.

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 은 DRM 메타데이터가 포함된 [!DNL .metadata] 파일입니다.

>[!NOTE]
>
>패키징 중에 Media Packager는 기본적으로 .header 파일을 더 이상 생성하지 않습니다. 이 파일을 생성하려면 패키지하는 동안 옵션을 `-h` 사용하십시오.

다음 표에는 위의 구문에 나와 있는 명령줄 옵션에 대한 설명이 나와 있습니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">명령줄 옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> 구성 파일 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">구성 파일의 위치를 지정합니다. 이 옵션을 사용하지 않으면 Media Packager에서 작업 디렉토리에서 flashaccesstools.properties <span class="filepath"> </span> 를 찾습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> 암호화 파일 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이미 패키지된 파일에 대한 정보를 표시합니다. 소스 파일과 대상 파일은 필요하지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadataffile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">기존 메타데이터에 대한 정보를 표시합니다. 소스 파일과 대상 파일은 필요하지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">패키지 파일에서 정책을 추출하려면 이 옵션 <span class="codeph"> 과 -d </span> 를 함께 사용하십시오. 파일 이름 및 정책 식별자를 사용하여 암호화된 파일과 같은 디렉토리에 파일이 만들어집니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">-d와 함께 <span class="codeph"> 사용하면 패키지된 파일 </span> 에서 DRM 헤더를 추출할 수 있습니다. 파일 이름 및 확장명을 사용하여 파일을 암호화된 파일과 동일한 디렉토리에 <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i content <span class="+ topic/ph pr-d/codeph codeph"> ID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">이 콘텐츠 부분에 대한 고유 식별자를 지정합니다. 식별자를 지정하지 않으면 대상 파일 이름이 사용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> 값 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">콘텐츠 메타데이터에 추가할 사용자 지정 키/값을 지정합니다. 다중 <span class="codeph"> -k </span> 옵션을 지정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">패키지 파일에서 메타데이터를 추출하려면 이 옵션 <span class="codeph"> 과 -d </span> 를 함께 사용하십시오. 파일 이름 및 확장자 .metadata를 사용하여 암호화된 파일과 같은 디렉토리에 파일이 <span class="codeph"> 생성됩니다 </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일을 덮어쓸지 여부를 묻지 않습니다. 대상 파일이 이미 있고 - <span class="codeph"> o를 설정하지 </span> 않으면 오류가 반환됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">대상 파일이 이미 있는 경우 묻지 않고 파일을 덮어씁니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 파일 이름 [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">정책을 포함하는 파일의 이름을 지정합니다. 정책에 속성 파일에 지정된 것과 다른 전송 인증서를 사용하는 서버에 도메인 등록이 필요한 경우 도메인 전송 인증서도 제공해야 합니다. </p> <p class="- topic/p ">다중 <span class="codeph"> -p </span> 옵션을 지정할 수 있으며, 클라이언트는 기본적으로 첫 번째 옵션을 사용합니다. 명령줄에 지정된 값이 구성 파일에 지정된 값보다 우선합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

