---
description: 우선 순위 규칙은 VAST/VMAP 응답에서 재생하기 위해 선택할 광고 크리에이티브의 우선 순위 순서를 정의합니다.
keywords: 우선순위 규칙;크리에이티브 선택 규칙
title: 우선 순위 규칙
exl-id: a045e102-1c16-46b5-8322-0bcab086ac67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 우선 순위 규칙{#priority-rules}

우선 순위 규칙은 VAST/VMAP 응답에서 재생하기 위해 선택할 광고 크리에이티브의 우선 순위 순서를 정의합니다.

## 우선순위 규칙에는 다음과 같은 속성과 가능한 값이 있습니다.

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 키</th> 
   <th class="entry"> 유형</th> 
   <th class="entry"> 값</th> 
   <th class="entry"> 설명</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 우선 순위</span></td> 
   <td><span class="codeph"> 배열</span></td> 
   <td></td> 
   <td> 재생을 위해 소스 크리에이티브를 선택해야 하는 우선 순위를 정의하는 소문자 mime 유형의 배열입니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 항목</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 호스트</span></td> 
   <td>현재는 <span class="codeph"> 호스트</span> 은(는) 지원됩니다. 이 속성은 다음과 같은 경우에 있어야 합니다. <span class="codeph"> 일치</span> 및 <span class="codeph"> 값</span> 속성이 정의됩니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 일치</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 복수</span></td> 
   <td>가능한 값:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - 다음과 같음</li> 
     <li><span class="codeph"> ne</span> - 같지 않음</li> 
     <li><span class="codeph"> co</span> - 포함</li> 
     <li><span class="codeph"> nc</span> - 포함하지 않음</li> 
     <li><span class="codeph"> sw</span> - 다음으로 시작</li> 
     <li><span class="codeph"> 새</span> - 다음으로 끝남</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 유형</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 우선 순위</span></td> 
   <td>값은 항상 다음과 같아야 합니다. <span class="codeph"> 우선 순위</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 값</span></td> 
   <td><span class="codeph"> 배열</span></td> 
   <td></td> 
   <td> <p>TVSDK는 <span class="codeph"> 일치</span> 속성 <span class="codeph"> 항목</span> 소스 크리에이티브 및 이 배열에 정의된 값과 일치</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 스트림</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td></td> 
   <td> <p>값은 다음과 같을 수 있습니다. <span class="codeph"> vod</span> 또는 <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```
