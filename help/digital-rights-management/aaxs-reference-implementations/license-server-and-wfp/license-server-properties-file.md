---
seo-title: 라이센스 서버 속성 파일
title: 라이센스 서버 속성 파일
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 라이센스 서버 속성 파일 {#license-server-properties-file}

이 [!DNL flashaccess-refimpl.properties] 파일을 사용하여 참조 구현의 라이센스 서버 구성 요소를 구성합니다. 적어도 전송 자격 증명 및 라이센스 서버 자격 증명과 관련된 속성을 구성해야 합니다. 자격 증명 파일의 위치는 `config.resourcesDirectory` 속성에 지정된 디렉토리에 상대적인 것으로 지정해야 합니다. 이 파일에는 패키지화 콘텐트와 관련된 여러 속성도 포함되어 있습니다.이러한 속성은 Flash Media Rights Management Server 1.x 메타데이터 변환에만 사용됩니다. 이 속성 파일의 값을 수정하는 경우 변경 사항을 적용하려면 라이센스 서버를 다시 시작해야 합니다.

Adobe Access에서 iOS 클라이언트에 원격 키 전달에 대한 라이선스 생성을 지원하려면 키 서버 인증서를 에 지정해야 합니다 [!DNL flashaccess-refimpl.properties].

다음 속성이 Adobe Access에 추가되었습니다.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">속성 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">설명 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> Adobe에서 발행한 키 서버의 라이센스 서버 인증서. 이 인증서는 메타데이터가 키 서버가 필수임을 나타내는 경우 iOS 장치의 라이센스를 생성하는 데 사용됩니다. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">HSM에 저장된 키 서버의 Adobe 발급 라이센스 서버 인증서의 별칭. HSM이 활성화되면 HandlerConfiguration.KeyServerCertificate 대신 이 속성을 <span class="codeph"> 사용합니다</span>. </td> 
  </tr> 
 </tbody> 
</table>

