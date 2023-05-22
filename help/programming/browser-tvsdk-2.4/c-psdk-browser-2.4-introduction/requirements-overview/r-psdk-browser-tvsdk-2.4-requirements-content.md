---
description: 스트림 및 재생 목록(매니페스트)에 대한 제한 사항 및 요구 사항을 확인하십시오.
title: 컨텐츠 및 매니페스트 요구 사항
exl-id: 53fdd771-06ea-496f-9591-6ed4d5011f8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 컨텐츠 및 매니페스트 요구 사항{#content-and-manifest-requirements}

스트림 및 재생 목록(매니페스트)에 대한 제한 사항 및 요구 사항을 확인하십시오.

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> 컨텐츠 세그먼트 기간 </td> 
   <td colname="col2"> 세그먼트의 기간은 매니페스트 파일에 지정된 대상 기간을 초과할 수 없습니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 콘텐츠 요구 사항 </td> 
   <td colname="col2"> 모든 TS 세그먼트는 키 프레임으로 시작해야 합니다. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> HLS 콘텐츠 </td> 
   <td colname="col2"> <p>다음 사항을 기억하십시오. 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">AAC-SSR 오디오가 지원되지 않습니다. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">오디오 코덱 AC3 및 고급 AC3은 지원되지 않습니다. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">불연속성이 있지만 불연속 마커가 없는 HLS 스트림은 지원되지 않습니다. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live는 타임스탬프 롤오버를 지원하지 않습니다. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">HLS 라이브 스트림의 DVR 창에 있는 광고가 확인되지 않습니다. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">바이트 범위는 AES-128 암호화 콘텐츠에서 지원되지 않습니다. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> DASH 콘텐츠 </td> 
   <td colname="col2"> <p>다음 사항을 기억하십시오. 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">라이브 스트림의 경우 - 동적 유형의 라이브 프로필이 지원됩니다. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">VOD 스트림의 경우 - 정적 유형의 라이브 프로필이 지원됩니다. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">VOD 스트림의 경우 - 주문형 프로필이 광고 워크플로우에 대해 인증되지 않았습니다. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">여러 기간이 있는 DASH 스트림 재생은 지원되지 않습니다. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">액세스 가능성 태그를 통해 신호로 표시되는 포함된 캡션(608/708)이 지원됩니다. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">단편화/세그먼트화된 VTT 파일은 지원되지 않습니다. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">인밴드 사용자 지정 태그가 있는 스트림은 인증되지 않았습니다. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>
