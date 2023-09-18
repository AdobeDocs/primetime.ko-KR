---
description: 다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 대체할 수 있습니다. 시그널링 모드와 메타데이터의 상이한 조합은 상이한 비헤이비어를 초래한다.
title: 광고 시그널링 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 광고 시그널링 모드 및 광고 메타데이터 조합에서 광고 삽입 및 삭제에 미치는 영향{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

다양한 광고 신호 모드 및 광고 메타데이터 조합을 사용하여 VOD 스트림의 시간 범위를 표시, 삭제 및 대체할 수 있습니다. 시그널링 모드와 메타데이터의 상이한 조합은 상이한 비헤이비어를 초래한다.

>[!NOTE]
>
>시간 범위와 광고 시그널링 모드 사이에 충돌이 있을 때, TVSDK는 시간 범위에 우선 순위를 부여한다.

**표 3: 시그널링 모드/메타데이터 조합 동작**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 광고 신호 모드 </th> 
   <th class="entry"> 광고 메타데이터 </th> 
   <th class="entry"> 해결자 생성됨 </th> 
   <th class="entry"><span class="codeph"> 배치 정보</span> 생성됨 </th> 
   <th class="entry"> 결과 비헤이비어 </th> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 범위 삭제됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 범위 삭제, 광고 삽입 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 광고 삽입됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.PLACEMENT), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)(DELETE 정보(Type.CUSTOM_TIME_RANGE, Mode.REPLACE))</span> </td> 
   <td> 범위 대체됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 범위가 표시되어 있고 광고가 삽입되지 않았습니다. </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> 광고 삽입됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 범위 삭제, 광고 삽입 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시, Auditude </td> 
   <td> 표시, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 범위가 표시되어 있고 광고가 삽입되지 않았습니다. </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제 </td> 
   <td> 삭제 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 범위 삭제됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.PLACEMENT), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)(DELETE 정보(Type.CUSTOM_TIME_RANGE, Mode.REPLACE))</span> </td> 
   <td> 범위 대체됨 </td> 
  </tr> 
  <tr> 
   <td> <b>사용자 정의 시간 범위</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제 </td> 
   <td> 삭제 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 범위 삭제됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 범위가 삭제되고 광고가 삽입되지 않음 </td> 
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
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.PLACEMENT), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)(DELETE 정보(Type.CUSTOM_TIME_RANGE, Mode.REPLACE))</span> </td> 
   <td> 범위가 광고로 대체됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시, Auditude </td> 
   <td> 사용자 지정 광고, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 범위가 표시되어 있고 광고가 삽입되지 않았습니다. </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 범위 삭제됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 삭제, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> DELETE PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.INSERT), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 범위 삭제, 광고 삽입 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 광고 삽입됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 바꾸기, Auditude </td> 
   <td> 삭제, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.PLACEMENT), PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)(DELETE 정보(Type.CUSTOM_TIME_RANGE, Mode.REPLACE))</span> </td> 
   <td> 범위가 광고로 대체됨 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 표시, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 표시된 범위 </td> 
  </tr> 
 </tbody> 
</table>
