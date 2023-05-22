---
description: 정규화 규칙은 VAST/VMAP 응답에서 가져온 소스 크리에이티브 URL에 적용할 URL 변환을 정의합니다.
keywords: 규칙 정규화;크리에이티브 선택 규칙
title: 규칙 정규화
exl-id: 731e0cfd-cabd-4e34-a01e-537c23be6a2d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 규칙 정규화 {#normalize-rules}

정규화 규칙은 VAST/VMAP 응답에서 가져온 소스 크리에이티브 URL에 적용할 URL 변환을 정의합니다.

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>키</b></th> 
   <th class="entry"><b>유형</b></th> 
   <th class="entry"><b>값</b></th> 
   <th class="entry"><b>설명</b></th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 유형</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 정규화</span></td> 
   <td>값은 항상 다음과 같아야 합니다. <span class="codeph"> 정규화</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 항목</span></td> 
   <td><span class="codeph"> 문자열</span></td> 
   <td><span class="codeph"> 호스트</span></td> 
   <td>현재는 <span class="codeph"> 호스트</span> 은(는) 지원됩니다. 이 속성은 다음과 같은 경우에 있어야 합니다. <span class="codeph"> 일치</span> 및 <span class="codeph"> 값</span> 속성이 정의됩니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 일치</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> 값</span></td> 
   <td><span class="codeph"> 배열</span></td> 
   <td></td> 
   <td>TVSDK는 <span class="codeph"> 일치</span> 속성 <span class="codeph"> 항목</span> 소스 크리에이티브 및 이 배열에 정의된 값과 일치</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 찾기</span></td> 
   <td><span class="codeph"> 정규 표현식</span></td> 
   <td></td> 
   <td> 일치시킬 소스 크리에이티브 URL에 적용할 정규 표현식입니다.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> 정규 표현식</span></td> 
   <td></td> 
   <td> 일치를 기반으로 바꿀 소스 크리에이티브 URL에 적용할 정규 표현식입니다.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```
