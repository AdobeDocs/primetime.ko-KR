---
title: 부록 B "디버깅 팁"
description: 부록 B "디버깅 팁"
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 부록 B: 디버깅 팁 {#appendix-b-debugging-tips}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.


## 임시 데이터 지우기 {#clearing-temporary-data}

Adobe Primetime 인증은 브라우저 캐시, LSO 캐시 및 쿠키와 같은 임시 데이터를 저장합니다. 테스트 시 깨끗한 슬레이트를 얻기 위해 임시 데이터를 삭제하는 것이 중요합니다.

- [브라우저 캐시 및 쿠키 지우기](#clearing-the-browser-cache-and-cookies)
- [LSO 캐시 지우기](#clearing-lsos-cache)\
    

## 브라우저 캐시 및 쿠키 지우기 {#clearing-the-browser-cache-and-cookies}

이것은 브라우저를 신뢰할 수 있지만 Firefox에서는 다음과 같습니다. &quot;Tools&quot; -\> &quot;최근 기록 지우기..&quot; -\> &quot;지울 시간 범위:&quot;에서 &quot;모두&quot;를 선택합니다. 그리고 &quot;세부 정보&quot;에서 &quot;Cookies&quot; 및 &quot;Cache&quot; -\> &quot;Clear Now&quot;를 클릭합니다.\
 

## LSO 캐시 지우기 {#clearing-lsos-cache}

액세스 권한 [Flash Player 도움말](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

을(를) 선택합니다 ```entitlement.\*``` (테스트 결과에 따라) &quot;웹 사이트 삭제&quot;를 클릭합니다.\
 

## 디버깅 도구 {#tools}

Adobe Primetime 인증 엔지니어는 다음 디버깅 도구를 사용합니다.

- Firebug - <http://www.getfirebug.com/>
- Flashbug(Flash Player의 디버그 버전에서 작동함) <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- 라이브 http 헤더 - <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->