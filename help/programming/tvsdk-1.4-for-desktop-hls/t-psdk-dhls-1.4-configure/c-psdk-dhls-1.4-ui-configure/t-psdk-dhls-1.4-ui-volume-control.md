---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
title: 볼륨 컨트롤 제공
exl-id: 058d79d2-35cc-4238-8fc1-2820a2d91ffb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 볼륨 컨트롤 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. MediaPlayer 인스턴스가 이 명령에 대해 유효한 상태가 될 때까지 기다리십시오.

   RELEASED를 제외한 모든 상태는 유효합니다.
1. 에서 볼륨 세트 메서드 호출 `MediaPlayer` 오디오 볼륨을 설정할 인스턴스입니다.

   ```
   public function set volume(value:Number):void
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타내며, 여기서 0은 묵음, 1은 최대 볼륨입니다.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 지정한 볼륨이 </th> 
      <th colname="col2" class="entry"> 결과 볼륨은 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 0 미만 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 0과 1 사이 </td> 
      <td colname="col2"> 지정한 볼륨 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 1보다 큼 </td> 
      <td colname="col2"> 값을 100으로 나눈 후 다음 값 중 하나로 설정합니다. 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">결과가 0과 1 사이인 경우 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">결과가 1보다 큰 경우 1 </li> 
      </ul> <p>팁: 이 논리는 이전 버전의 
      <span class="codeph">phrases/primetime-sdk-name</span>여기서 볼륨 값은 0에서 100 사이입니다. </p> </td> 
   </tr> 
   </tbody> 
   </table>
