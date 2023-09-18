---
title: 출력 보호 제어
description: 출력 보호 제어
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 출력 보호 제어 {#output-protection-controls}

**외부 렌더링 장치로의 출력을 보호할지 여부를 제어합니다. 아날로그 및 디지털 출력을 독립적으로 지정합니다.**

외부 렌더링 장치로의 출력을 제한할지 여부를 제어합니다. 외부 장치는 컴퓨터에 임베드되지 않은 비디오 또는 오디오 장치로 정의됩니다. 외부 장치 목록에는 노트북 컴퓨터에서와 같이 통합 디스플레이가 제외됩니다. 아날로그 및 디지털 출력 제한은 독립적으로 지정할 수 있습니다.

다음 옵션/적용 수준을 사용할 수 있습니다.

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">옵션 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">아날로그 장치에서 지원됨 </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">디지털 장치에서 지원됨 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">필수</b> — ACP(Analog Copy Protection) 또는 CGMS(Copy Generation Management System) - 컨텐츠를 외부 장치에 재생하려면 아날로그(CGMS-A) 출력 보호를 활성화해야 합니다. Adobe 액세스 클라이언트는 ACP 또는 CGMS-A를 사용하여 출력 보호를 활성화해야 합니다. 둘 다 지원하는 장치에서 Adobe 액세스 3.0 클라이언트는 둘 다 활성화하려고 시도합니다. 단, 콘텐츠를 재생하려면 하나만 활성화해야 합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP 필요</b> — ACP 출력 보호가 필요합니다. CGMS-A에서는 재생이 허용되지 않습니다. Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정하면 Adobe 액세스 2.0 클라이언트가 "재생 없음" 옵션이 지정된 것처럼 동작합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A 필요</b> — CGMS-A 출력 보호가 필요합니다. ACP에서 재생이 허용되지 않습니다. Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정하면 Adobe 액세스 2.0 클라이언트가 "재생 없음" 옵션이 지정된 것처럼 동작합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">사용 가능한 경우 사용</b> — 사용 가능한 경우 ACP 및 CGMS-A 출력 보호를 활성화하고 사용 불가능한 경우 재생을 허용합니다. Adobe 액세스 3.0 클라이언트는 가능한 경우 ACP와 CGMS-A 모두를 활성화하려고 시도합니다. Adobe 액세스 2.0 클라이언트는 ACP 또는 CGMS-A만 활성화하려고 합니다. 예를 들어 Adobe 액세스 클라이언트가 ACP 또는 CGMS-A를 사용으로 설정하려고 합니다. 시도가 성공하면 다른 옵션은 활성화되지 않습니다. 시도가 실패하면 다른 옵션을 활성화하기 위해 두 번째 시도가 수행됩니다. 두 번의 시도가 모두 실패하더라도 콘텐츠는 어쨌든 재생됩니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">가능한 경우 ACP 사용</b> — 사용 가능한 경우 ACP 출력 보호를 활성화하지만 사용 불가능한 경우 재생을 허용합니다. CGMS-A에서는 보호를 사용할 수 없습니다. Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정하면 Adobe 액세스 2.0 클라이언트가 "보호 없음" 옵션이 지정된 것처럼 동작합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">가능한 경우 CGMS-A 사용 </b>— 사용 가능한 경우 CGMS-A 출력 보호를 활성화하지만 사용 불가능한 경우 재생을 허용합니다. ACP에서 보호를 사용할 수 없습니다. Adobe 액세스 2.0 클라이언트는 이 옵션을 지원하지 않습니다. 설정하면 Adobe 액세스 2.0 클라이언트가 "보호 없음" 옵션이 지정된 것처럼 동작합니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">보호 없음</b> — 아날로그 및 디지털 출력에 대해 출력 보호 기능이 적용되지 않습니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">재생 없음</b> - 외부 장치에서 아날로그 및 디지털 출력을 재생할 수 없습니다. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">예 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>이러한 규칙은 모든 플랫폼에 일관되게 적용되지만, 현재는 Windows 플랫폼에서만 안전하게 출력 보호를 켤 수 있습니다. 다른 플랫폼(예: Macintosh 및 Linux)에서는 서드파티 애플리케이션에서 사용할 수 있는 운영 체제 기능이 없습니다.

사용 사례: 일부 컨텐츠는 출력 보호 제어를 적용할 수 있으며, 컨텐츠 배포자가 보호 수준을 설정할 수 있습니다. &quot;필수&quot;를 지정하고 Macintosh에서 재생을 시도하면 클라이언트가 외부 장치에서 컨텐츠를 재생하지 않습니다. 그러나 콘텐츠는 내부 모니터에서 재생됩니다.

&quot;필수&quot;를 지정하고 Linux에서 재생을 시도하면 클라이언트가 내부 장치와 외부 장치를 구별할 수 없으므로 장치에서 컨텐츠를 재생하지 않습니다.

&quot;사용 가능한 경우&quot;를 지정하면 가능하면 출력 보호가 켜집니다. 예를 들어 COPP(Certified Output Protection Protocol)를 지원하는 Windows 시스템의 경우 콘텐츠가 출력 보호와 함께 외부 디스플레이에 전달됩니다. 이러한 예를 &quot;선택 가능한 출력 제어&quot;라고도 합니다.
