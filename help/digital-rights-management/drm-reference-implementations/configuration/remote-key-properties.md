---
title: 원격 키 배달 속성(iOS)
description: 원격 키 배달 속성(iOS)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 원격 키 배달 속성(iOS){#remote-key-delivery-properties-ios}

Adobe Primetime DRM에서 iOS 클라이언트에 원격 키 전달에 대한 라이선스 생성을 지원하려면 `flashaccess-refimpl.properties` 파일에 키 서버 인증서를 지정해야 합니다.

다음 속성이 Primetime DRM에 추가되었습니다.

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
   <td colname="2" class="- topic/entry "> <p>Adobe에서 발행한 키 서버의 라이센스 서버 인증서 </p> <p>이 인증서는 키 서버가 필수임을 메타데이터에 나타낼 때 iOS 장치에 대한 라이센스를 생성합니다. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>HSM에 저장된 키 서버의 Adobe 발급 라이선스 서버 인증서의 별칭 </p> <p>HSM을 활성화하면 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> 속성 대신 이 속성을 적용할 수 있습니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

