---
title: 환경 설정 개요 설정
description: 환경 설정 개요 설정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 환경 설정 개요 {#setting-preferences-overview} 설정

Packager 서버 URL을 제외하고 아래에 지정된 모든 환경 설정이 서버의 [!DNL flashaccess-refimpl-packager.properties] 파일에 저장됩니다. 모든 설정은 속성 파일에서 직접 또는 AIR 응용 프로그램을 통해 수정할 수 있습니다. 암호는 서버의 속성 파일에 저장될 때 암호화됩니다. 암호화되지 않은 암호를 UI에 입력하면 파일에 저장되기 전에 암호화됩니다.

>[!NOTE]
>
>모든 디렉토리 및 경로는 AIR 응용 프로그램을 실행하는 클라이언트가 아닌 패키지 서버 상의 디렉토리를 참조합니다.

여기에서 수행된 모든 변경 사항은 환경 설정이 저장되면 즉시 적용됩니다. 구성 문제로 인해 패키지 스레드가 종료되지 않으면 서버를 다시 시작할 필요가 없습니다.

기본 설정 설명에 다음과 같은 용어가 사용됩니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 환경 설정 </th> 
   <th colname="2" class="- topic/entry entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 패키지 서버 URL </td> 
   <td colname="2" class="- topic/entry "> <span class="filepath"> flashaccess-packager.war </span>;을(를) 실행하는 서버 위치예를 들어 <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 리소스 디렉토리 </td> 
   <td colname="2" class="- topic/entry "> 정책, 인증서, 자격 증명 및 패키지 서버에 필요한 기타 리소스가 포함된 디렉토리 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 라이선스 서버 URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트가 라이센스를 요청해야 하는 서버의 URL;예를 들어 <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

