---
description: 'null'
seo-description: 'null'
seo-title: 보호된 내용을 재생하는 데 필요한 장치 기능
title: 보호된 내용을 재생하는 데 필요한 장치 기능
uuid: 1490711b-65d9-4716-8779-ae1da7d2c82c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 보호된 내용을 재생하는 데 필요한 장치 기능 {#device-capabilities-required-to-play-protected-content}

필요한 장치 기능은 컨텐츠에 액세스하는 데 필요한 하드웨어 기능을 지정합니다. 하드웨어 기능에 대한 정보는 포팅 키트를 사용하는 장치에 사용할 수 있습니다.

다음 속성은 장치 기능을 식별할 수 있습니다.

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>속성</b> </td> 
   <td><b>지원되는 값</b> </td> 
   <td><b>일치 기준</b> </td> 
   <td><b>설명</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">사용자가 액세스할 수 없는 버스 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" 또는 "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">정확히 일치 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">true이면 장치에 사용자가 액세스할 수 있는 버스가 없어야 합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">신뢰의 하드웨어 루트 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" 또는 "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">정확히 일치 </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">true이면 장치에 하드웨어 신뢰 루트가 있어야 합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>이 사용 규칙은 Adobe Primetime DRM 클라이언트 버전 2.0.2 이상에서 지원됩니다. 이전 클라이언트의 동작은 라이센스 서버에서 지원하는 최소 클라이언트 버전에 따라 달라집니다.
>
>최소 [클라이언트 버전을 참조하십시오](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).

