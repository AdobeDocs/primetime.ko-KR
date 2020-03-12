---
seo-title: 환경 설정 개요
title: 환경 설정 개요
uuid: d1c067b1-6c2b-460e-8d00-5a5bfee0789c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 환경 설정 개요 {#setting-preferences-overview}

Packager Server URL을 제외하고, 아래에 지정된 모든 환경 설정이 서버의 [!DNL flashaccess-refimpl-packager.properties] 파일에 저장됩니다. 모든 설정은 속성 파일에서 직접 또는 AIR 애플리케이션을 통해 수정할 수 있습니다. 암호는 서버의 속성 파일에 저장될 때 암호화됩니다. 암호화되지 않은 암호를 UI에 입력하면 파일에 저장되기 전에 암호화됩니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>모든 디렉토리 및 경로는 AIR 애플리케이션을 실행하는 클라이언트가 아닌 패키지 서버의 디렉토리를 나타냅니다.

여기에서 수행된 모든 변경 사항은 환경 설정이 저장되면 즉시 적용됩니다. 구성 문제로 인해 Packager 스레드가 종료되지 않으면 서버를 다시 시작할 필요가 없습니다.

기본 설정 설명에 다음 용어가 사용됩니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 기본 설정 </th> 
   <th colname="2" class="- topic/entry entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 패키지 서버 URL </td> 
   <td colname="2" class="- topic/entry "> flashaccess-packager.war를 실행하는 서버 <span class="filepath"> 위치 </span>;예를 들어, https://localhost:8080과 <span class="filepath"> 같이 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 리소스 디렉토리 </td> 
   <td colname="2" class="- topic/entry "> 정책, 인증서, 자격 증명 및 패키지 서버에 필요한 기타 리소스가 포함된 디렉토리 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 라이선스 서버 URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">클라이언트가 라이센스를 요청해야 하는 서버의 URL;예를 들어, https://mylicenseserver.com:8080과 <span class="filepath"> 같이 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

