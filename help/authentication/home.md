---
title: Adobe(&R) 시작 Primetime 인증
description: Adobe(&R) 시작 Primetime 인증 개요
source-git-commit: 79cdd0b7ae33d7c1d2bec970ecd3654aea4fdab0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe® Primetime 인증 시작 {#overview}

Adobe Primetime 인증은 TV Everywhere의 자격 해결 방법이며, 리소스에 대한 액세스를 요청하는 사람에게 권한이 있는지 여부를 결정하는 모듈식 프레임워크를 제공합니다. Primetime 인증 자격 부여 솔루션에 참여하기 위해 컨텐츠 공급자(프로그래머) 및 MVPD(유료 TV 공급자)는 자격 부여 시스템을 Primetime 인증 워크플로우와 통합합니다. 이 설명서 사이트에서는 통합 프로세스에 대한 세부 사항과 기존 파트너를 위한 팁을 제공합니다.

여러분의 의견은 항상 감사합니다.

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

## 많이 사용하는 도움말 및 FAQ {#help-and-faqs-resources}

|중요 항목| |-| |<ul>&lt;>iOS용 단일 사인온 Infographic Primetime TVE Dashboard 사용 안내서|

| 프로그래머용 | MVPD용 |
|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| <ul><li>Programmer Kickstart 안내서</li><li> MVPD 선택기(&quot;선택기&quot;)</li><li>사용자 메타데이터</li></ul> | <ul><li>MVPD 시작 안내서</li><li>인증</li><li>인증</li><li>로그아웃</li></ul> |
| **기본 앱 클라이언트의 경우** | **모든 사용자** |
| <ul><li>iOS 기술 개요</li><li>Android 기술 개요</li></ul> | <ul><li>기술 문서</li><li>에스컬레이션 절차</li><li>지원되는 시스템</li><li>용어 설명</li><li>기술 노트</li></ul> |
| 스마트 장치용 |  |
| <ul><li>Clientless 기술 개요</li><li>Clientless API</li></ul> |

<div id="startcontainer">

<div class="table">

<table id="start-topic-table" data-border="0" data-cellpadding="0" data-cellspacing="0" style="height: 380px; width: 584px;">
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">인기 있는 도움말 및 FAQ</th>
<th style="text-align: left;"> </th>
<th style="text-align: left;"> </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p><strong>프로그래머용</strong></p>
<p> </p>
<ul>
<li><a href="#">Programmer Kickstart 안내서</a></li>
</ul>
<ul>
<li><a href="#obtaining_mvpd_list">MVPD 선택기("선택기")</a></li>
<li><a href="#">사용자 메타데이터</a></li>
</ul>
 
<p><strong>기본 앱 클라이언트의 경우</strong></p>
<ul>
<li><a href="#">iOS 기술 개요</a></li>
<li><a href="#">Android 기술 개요</a></li>
</ul>
<p> </p>
<p><strong>스마트 장치용</strong></p>
<ul>
<li><a href="http://tve.helpdocsonline.com/rest-api-overview">Clientless 기술 개요</a></li>
<li><a href="https://tve.helpdocsonline.com/rest-api-reference">Clientless API</a></li>
</ul>
<p> </p></td>
<td style="text-align: left;"><p><strong>MVPD용</strong></p>
<p> </p>
<ul>
<li><a href="#">MVPD 시작 안내서</a></li>
<li><a href="#">인증</a></li>
<li><a href="#">인증</a></li>
</ul>
<ul>
<li><a href="#">로그아웃</a></li>
</ul>
 
<p><strong>모든 사용자</strong></p>
<ul>
<li><a href="#">기술 문서</a></li>
<li><a href="#">에스컬레이션 절차</a></li>
<li><a href="#">지원되는 시스템</a></li>
<li><a href="#">용어 설명</a></li>
<li><a href="#">기술 노트</a></li>
</ul></td>
<td style="text-align: left;"><p><strong>중요 항목 <img src="https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/1468939180_new.png?dc=201607190941-4" /></strong></p>
<p> </p>
<ul>
<li><a href="http://tve.helpdocsonline.com/ios/tvos-sso-changes">iOS용 단일 사인온</a></li>
<li><a href="#">프로모션 임시 패스</a></li>
<li><a href="#">홈 기반 인증(HBA)</a></li>
<li><a href="https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf">HBA 인포그래픽</a></li>
<li><a href="#">Primetime TVE 대시보드 사용 안내서</a></li>
</ul></td>
</tr>
</tbody>
</table>

</div>

<div class="block">

## 답을 찾을 수 없습니까?

[**이메일**](mailto:tve-support@adobe.com)

[지원 팀에 이메일 보내기](mailto:tve-support@adobe.com) 또한 문제 또는 사고 보고서의 첫 번째 단계입니다.

만약 [**<span style="color:#ff0000;">심각도 1 라이브</span>**](http://tve.helpdocsonline.com/escalation-procedures-2)
문제가 발생하여 e-메일로 보내셨고 30분이 지나갔습니다\
응답 없이\
[에스컬레이션 절차](#) 문서\
전화 번호 조회

<div>

 

</div>

</div>

</div>

 

<span style="font-family: verdana, geneva, sans-serif;">필요한 항목을 찾으려면</span>

<span style="font-family: verdana, geneva, sans-serif;">** **   **검색** 이 설명서를 포함하는 결과는 Primetime 인증 헬프데스크에 문의하십시오.\
     **찾아보기** 왼쪽 탐색 창에서 폴더 계층 구조를 통해 모든 Primetime 인증 문서.\
     **필터** 탐색 창 위쪽에 있는 필드에 용어를 입력하여 폴더 계층 구조에 대해 설명합니다.\
     **북마크** 웹 브라우저를 사용하여 관심 페이지에 대한 &quot;딥 링크&quot;입니다.</span>
