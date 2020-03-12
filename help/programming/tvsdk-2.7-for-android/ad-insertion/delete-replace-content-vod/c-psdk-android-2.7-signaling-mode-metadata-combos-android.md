---
description: 다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터가 서로 다른 조합으로 인해 다른 동작이 발생합니다.
seo-description: 다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터가 서로 다른 조합으로 인해 다른 동작이 발생합니다.
seo-title: 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향
title: 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향
uuid: 7b2a5588-110d-4ce5-aa9c-706d357f211d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향 {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터가 서로 다른 조합으로 인해 다른 동작이 발생합니다.

>[!TIP]
>
>시간 범위와 광고 신호 모드 간에 충돌이 발생하는 경우 TVSDK는 시간 범위 우선 순위를 제공합니다.

다음 표에서는 신호 모드 및 메타데이터 조합 동작에 대한 세부 사항을 제공합니다.

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
 <thead> 
  <tr> 
   <th class="entry"> 광고 신호 모드 </th> 
   <th class="entry"> 광고 메타데이터 </th> 
   <th class="entry"> 만든 해상도 </th> 
   <th class="entry"><span class="codeph"> 배치정보</span> 생성 </th> 
   <th class="entry"> 결과 동작 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <p><b>서버 맵</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> 삭제 </td> 
   <td> 삭제 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 삭제된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td> 
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 삭제된 범위, 삽입된 광고 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 삽입된 광고 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 대체된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위, 삽입된 광고 없음 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>매니페스트 큐</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> 삽입된 광고 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td> 
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 삭제된 범위, 삽입된 광고 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위, 삽입된 광고 없음 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제 </td> 
   <td> 삭제 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 삭제된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 대체된 범위 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>사용자 지정 시간 범위</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제 </td> 
   <td> 삭제 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 삭제된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 삭제된 범위, 삽입된 광고 없음 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> 없음 </td> 
   <td> 삽입된 광고 없음 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 광고로 대체된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> 사용자 정의 광고, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위, 삽입된 광고 없음 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>설정되지 않음(기본값)</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제 </td> 
   <td> 삭제 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 삭제된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 삭제된 범위, 삽입된 광고 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 삽입된 광고 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 광고로 대체된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
 </tbody> 
</table>

