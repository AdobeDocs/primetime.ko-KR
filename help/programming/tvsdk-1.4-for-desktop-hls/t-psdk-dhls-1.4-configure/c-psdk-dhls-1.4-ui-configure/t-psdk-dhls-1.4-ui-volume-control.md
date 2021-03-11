---
description: 사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.
title: 볼륨 제어 제공
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 볼륨 컨트롤 제공{#provide-volume-control}

사운드 볼륨에 대한 사용자 인터페이스 컨트롤을 설정할 수 있습니다.

1. MediaPlayer 인스턴스가 이 명령에 대해 유효한 상태가 될 때까지 기다립니다.

   RELEASED를 제외한 모든 상태는 유효합니다.
1. `MediaPlayer` 인스턴스의 볼륨 집합 메서드를 호출하여 오디오 볼륨을 설정합니다.

   ```
   public function set volume(value:Number):void
   ```

   볼륨의 값은 최대 볼륨의 비율로 표현되는 요청된 볼륨을 나타냅니다. 여기서 0은 묵음이고 1은 최대 볼륨입니다.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 지정된 볼륨이 </th> 
      <th colname="col2" class="entry"> 결과 볼륨은 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> 0보다 작음 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 0에서 1 사이 </td> 
      <td colname="col2"> 지정된 볼륨 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> 1보다 큼 </td> 
      <td colname="col2"> 값을 100으로 나눈 후 다음 값 중 하나로 설정합니다. 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">0과 1 사이의 결과입니다. </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1보다 큰 경우 </li> 
      </ul> <p>팁: 이 논리는 
      <span class="codeph">구문/primetime-sdk-name</span>. 여기서 볼륨 값은 0부터 100까지입니다. </p> </td> 
   </tr> 
   </tbody> 
   </table>
