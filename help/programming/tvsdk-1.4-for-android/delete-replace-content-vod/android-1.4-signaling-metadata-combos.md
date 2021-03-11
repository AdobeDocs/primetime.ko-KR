---
description: 다른 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터의 서로 다른 조합으로 인해 다른 동작이 발생합니다.
title: 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# 광고 신호 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

다른 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 바꿀 수 있습니다. 신호 모드와 메타데이터의 서로 다른 조합으로 인해 다른 동작이 발생합니다.

>[!NOTE]
>
>시간 범위와 광고 신호 모드 간에 충돌이 발생하는 경우 TVSDK는 시간 범위 우선 순위를 제공합니다.

**표 3:신호 모드/메타데이터 조합 비헤이비어**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 광고 신호 모드 </th> 
   <th class="entry"> 광고 메타데이터 </th> 
   <th class="entry"> 만든 해상도 </th> 
   <th class="entry"><span class="codeph"> 배치 </span> 정보설명 </th> 
   <th class="entry"> 결과 동작 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>서버 맵</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
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
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </li> 
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
   <td> 범위가 대체됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 마크 </td> 
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
   <td> <b>매니페스트 큐</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
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
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </li> 
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
   <td> 마크 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 범위가 대체됨 </td> 
  </tr> 
  <tr> 
   <td> <b>사용자 지정 시간 범위</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
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
   <td> 삭제된 범위, 광고가 삽입되지 않음 </td> 
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
   <td> 마크 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> 사용자 지정 광고, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위, 삽입된 광고 없음 </td> 
  </tr> 
  <tr> 
   <td> <b>설정되지 않음(기본값)</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
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
   <td> 마크 </td> 
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

