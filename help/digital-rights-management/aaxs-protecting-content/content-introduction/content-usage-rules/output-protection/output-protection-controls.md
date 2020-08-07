---
seo-title: 출력 보호 제어
title: 출력 보호 제어
uuid: 1f4cc617-7f14-4952-8e61-6acbdf01d10e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# 출력 보호 제어 {#output-protection-controls}

**외부 렌더링 장치로의 출력 보호 여부를 제어합니다. 아날로그 및 디지털 출력을 독립적으로 지정합니다.**

외부 렌더링 장치로의 출력을 제한할지 여부를 제어합니다. 외부 장치는 컴퓨터에 임베드되지 않은 비디오 또는 오디오 장치로 정의됩니다. 외부 장치 목록은 노트북 컴퓨터 등의 통합 디스플레이를 제외합니다. 아날로그 및 디지털 출력 제한은 별도로 지정할 수 있습니다.

다음 옵션/적용 수준을 사용할 수 있습니다.

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">아날로그 장치에서 지원 </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">디지털 장치에서 지원 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">필수</b> — ACP(아날로그 복사 방지) 또는 복사 생성 관리 시스템 - 아날로그(CGMS-A) 출력 보호 기능이 활성화되어 외부 장치에 컨텐츠를 재생해야 합니다. Adobe 액세스 클라이언트는 ACP 또는 CGMS-A를 사용하여 출력 보호를 활성화해야 합니다.두 가지 모두를 지원하는 장치에서는 Adobe Access 3.0 클라이언트가 두 가지 모두를 활성화하려고 시도합니다. 그러나 컨텐츠를 재생하려면 하나만 활성화되어야 합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP 필수</b> — ACP 출력 보호가 필요합니다. CGMS-A에서는 재생할 수 없습니다.Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정된 경우 Adobe Access 2.0 클라이언트는 "재생 없음" 옵션이 지정된 것처럼 작동합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A 필수</b> — CGMS-A 출력 보호가 필요합니다. ACP에서 재생할 수 없습니다. Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정된 경우 Adobe Access 2.0 클라이언트는 "재생 없음" 옵션이 지정된 것처럼 작동합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">사용 가능한 경우</b> — 사용 가능한 경우 ACP 및 CGMS-A 출력 보호를 활성화하고 사용할 수 없는 경우 재생을 허용합니다. Adobe 액세스 3.0 클라이언트는 가능한 경우 ACP와 CGMS-A를 모두 활성화하려고 시도합니다. Adobe 액세스 2.0 클라이언트는 ACP 또는 CGMS-A를 활성화만 시도합니다.예를 들어 Adobe 액세스 클라이언트가 ACP 또는 CGMS-A를 활성화하려고 시도합니다.시도가 성공하면 다른 옵션이 활성화되지 않습니다. 시도가 실패하면 다른 옵션을 활성화하기 위해 두 번째 시도가 수행됩니다. 두 시도가 모두 실패하더라도 컨텐츠가 재생됩니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">사용 가능한</b> 경우 ACP 사용 — 사용 가능한 경우 ACP 출력 보호를 활성화하지만 사용 가능한 경우 재생을 허용하십시오. CGMS-A에서는 보호를 받을 수 없습니다.Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정된 경우 Adobe 액세스 2.0 클라이언트는 "보호 없음" 옵션이 지정된 것처럼 작동합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A 사용(가능한 경우) </b>— CGMS-A 출력 보호 기능을 활성화하지만 사용 가능한 경우 재생을 허용합니다. ACP에서는 보호를 사용할 수 없습니다. Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정된 경우 Adobe 액세스 2.0 클라이언트는 "보호 없음" 옵션이 지정된 것처럼 작동합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">보호</b> 없음 — 아날로그 및 디지털 출력 시 출력 보호 기능이 적용되지 않습니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">재생</b> 안 함 —아날로그 및 디지털 출력을 위해 외부 디바이스에 재생을 허용하지 마십시오. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>이러한 규칙은 모든 플랫폼에서 일관되게 적용되지만 현재 Windows 플랫폼에서 출력 보호를 안전하게 켜는 경우에만 가능합니다. 다른 플랫폼(예: Macintosh 및 Linux)에서는 타사 애플리케이션에서 사용할 수 있는 지원 운영 체제 기능이 없습니다.

사용 사례 예:일부 컨텐츠는 출력 보호 제어를 강제 할 수 있으며, 컨텐츠 배포자는 보호 수준을 설정할 수 있습니다. &quot;필수&quot;가 지정되어 있고 Macintosh에서 재생을 시도해도 클라이언트가 외부 장치의 컨텐츠를 재생하지 않습니다. 그러나 내용은 내부 모니터에서 재생됩니다.

&quot;필수&quot;가 지정되어 있고 Linux에서 재생을 시도해도 클라이언트는 내부 및 외부 장치를 구별할 수 없으므로 어떤 장치에서도 컨텐츠를 재생하지 않습니다.

&quot;사용 가능한 경우 사용&quot;을 지정하면 가능한 경우 출력 보호가 설정됩니다. 예를 들어 COP(Certified Output Protection Protocol)를 지원하는 Windows 시스템에서 외부 디스플레이로 출력 보호와 함께 내용이 전달됩니다. 이 예제는 &quot;선택 가능한 출력 제어&quot;라고도 합니다.
