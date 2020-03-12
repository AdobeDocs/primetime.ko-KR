---
description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-description: 기본 광고 동작을 사용하도록 선택할 수 있습니다.
seo-title: 기본 재생 동작 사용
title: 기본 재생 동작 사용
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 기본 재생 동작 사용{#use-the-default-playback-behavior}

기본 광고 동작을 사용하도록 선택할 수 있습니다.

기본 동작을 사용하려면:

    * &#39;ContentFactory&#39; 클래스를 구현하는 경우 &#39;doRetrieveAdPolicySelector&#39; 구현에서 &#39;DefaultAdPolicySelector&#39;의 새 인스턴스를 반환합니다.
    
    &quot;
    public class CustomContentFactory extends ContentFactory {
    
    //....
    // 광고 클래스에 대한 사용자 지정 코드
    //...
    
    /**
    ** @inheritDoc
    */
    override protected
    functiondoRetrieveAdPolicySelector(item:MediaPlayerItem):PolicySelector {
    return new AddAdSelectorDefault(item;;item}}
    
    
    
    
    }추가 사용자 정의 구현이 없는 경우\nFactory &#39; 클래스에서는 TVSDK에서 &#39;DefaultAdPolicySelector&#39;를 사용합니다.