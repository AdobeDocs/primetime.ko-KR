---
description: LoadInformation 클래스에서 조각 및 트랙과 같은 다운로드한 리소스에 대한 QoS(서비스 품질) 정보를 읽을 수 있습니다.
title: 로드 정보를 사용하여 조각 수준에서 추적
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 로드 정보를 사용하여 조각 수준에서 추적{#track-at-the-fragment-level-using-load-information}

LoadInformation 클래스에서 조각 및 트랙과 같은 다운로드한 리소스에 대한 QoS(서비스 품질) 정보를 읽을 수 있습니다.

1. 구현 `onLoadInformationAvailable` 콜백 이벤트 리스너입니다.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 조각이 다운로드될 때마다 TVSDK가 호출하는 이벤트 리스너를 등록합니다.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 에서 관심 데이터 읽기 `LoadInformation` 콜백에 전달됩니다.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 속성 </th> 
      <th colname="col1" class="entry"> 유형 </th> 
      <th colname="col2" class="entry"> 설명 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>숫자 </p> </td> 
      <td colname="col2"> <p>다운로드 기간(밀리초)입니다. </p> <p>TVSDK는 클라이언트가 서버에 연결하는 데 걸린 시간과 전체 조각을 다운로드하는 데 걸린 시간을 구분하지 않습니다. 예를 들어 10MB 세그먼트가 다운로드하는 데 8초가 걸리는 경우 TVSDK는 해당 정보를 제공하지만, 첫 번째 바이트까지 4초가 걸리고 전체 조각을 다운로드하는 데 4초가 걸렸다는 정보는 제공하지 않습니다. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>숫자 </p> </td> 
      <td colname="col2"> 다운로드한 조각의 미디어 기간(밀리초)입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 크기 </span> </td> 
      <td colname="col1"> <p>숫자 </p> </td> 
      <td colname="col2"> 다운로드한 리소스의 크기(바이트)입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 해당 트랙의 인덱스입니다(알고 있는 경우). 그렇지 않은 경우 0입니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 해당 트랙의 이름(알려진 경우). 그렇지 않은 경우 null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 해당 트랙의 유형(알고 있는 경우). 그렇지 않은 경우 null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 유형 </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> TVSDK에서 다운로드한 내용입니다. 다음 중 하나: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST - 재생 목록/매니페스트 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">조각 - 조각 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - 특정 트랙과 연결된 조각 </li> 
      </ul> 리소스 유형을 감지하지 못할 수도 있습니다. 이 경우 FILE이 반환됩니다. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>문자열 </p> </td> 
      <td colname="col2"> 다운로드한 리소스를 가리키는 URL입니다. </td> 
   </tr> 
   </tbody> 
   </table>
