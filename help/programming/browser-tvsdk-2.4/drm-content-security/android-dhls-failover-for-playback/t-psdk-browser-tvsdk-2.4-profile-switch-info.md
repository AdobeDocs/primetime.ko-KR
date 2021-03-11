---
description: 미디어 플레이어에서 현재 프로필을 새 프로필로 전환하면 전환의 전환시기, 폭 및 높이 정보 또는 다른 비트 전송률을 사용한 이유를 비롯하여 스위치에 대한 정보를 검색할 수 있습니다.
title: 프로필 스위치에 대한 정보 얻기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# 프로필 스위치{#get-information-about-profile-switch}에 대한 정보 가져오기

미디어 플레이어에서 현재 프로필을 새 프로필로 전환하면 전환의 전환시기, 폭 및 높이 정보 또는 다른 비트 전송률을 사용한 이유를 비롯하여 스위치에 대한 정보를 검색할 수 있습니다.

1. `AdobePSDK.PSDKEventType.PROFILE_CHANGED` 이벤트를 수신합니다.

   Browser TVSDK 미디어 플레이어는 네트워크나 컴퓨터 조건 때문에 응용 비트 전송률 전환 알고리즘이 다른 프로파일로 전환될 때 이 이벤트를 전달합니다. (비트 전송률 또는 기간이 변경되면)
1. 이벤트가 발생하면 스위치에 대한 자세한 내용은 다음 속성을 확인하십시오.

   * `profile`:사용 중인 새 프로필의 식별자입니다.
   * `time`:스위치가 발생한 스트림 시간입니다.
   * `description`:세미콜론으로 구분된 키/값 쌍의 문자열로, 비트 전송률 변경 이유에 대한 텍스트 설명입니다. 최대 1개의 `Reason` 및 1개의 `Bitrate`을 포함합니다. 정보를 사용할 수 없거나 비트 전송률이 변경되지 않은 경우 이 문자열은 비어 있습니다.

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 키 이름 </th> 
      <th colname="col2" class="entry"> 가능한 값 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 이유  </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">네트워크 적용 </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">검색 </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">지원되지 않는 프로필 </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">페일오버 </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 비트 전송률  </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> up  </span>:비트 전송률 증가 </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> 다운  </span>:비트 전송률이 감소했습니다. </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   다음은 반환된 `description` 문자열의 몇 가지 예입니다.

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`:너비를 픽셀 단위로 나타내는 정수입니다.
   * `height`:높이를 픽셀 단위로 나타내는 정수.

   >[!NOTE]
   >
   >폭 및 높이 데이터는 M3U8 매니페스트의 `RESOLUTION` 태그에 포함된 경우에만 사용할 수 있습니다. 정보가 M3U8에 포함되지 않은 경우 프로파일 정보에 포함되지 않으므로 폭 및 높이 속성이 0으로 설정됩니다.
