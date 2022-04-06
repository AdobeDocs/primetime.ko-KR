---
title: 계정 IQ가 계정 IQ, 사전 요구 사항 및 온보딩으로 시작됩니다
description: '계정 IQ를 온보드, 사전 요구 사항 및 시작하는 방법. '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# 계정 IQ를 시작하는 방법 {#onboarding}

계정 IQ를 사용하기 위한 사전 요구 사항과 구독자의 계정 공유 점수를 확인하기 위해 고객이 온보딩하는 방법을 숙지하십시오.

## 전제 조건 {#prerequisites}

* 조직을 [!DNL Adobe Marketing Cloud] 조직

* 해당 조직의 사용자는 TVE 대시보드 읽기-쓰기 또는 TVE 대시보드 읽기 전용으로 할당해야 합니다.

### 브라우저 사전 요구 사항 {#browser-prerequisites}

계정 IQ는 호스팅된 웹 서비스입니다. 이 브라우저는 다음 브라우저의 최신 버전과 호환됩니다.

* Google Chrome
* Mozilla Firefox
* Safari 버전

### 계정 IQ에서 조직을 온보딩하는 방법 {#steps-to-onboard}


이것이 현재 우리가 가지고 있는 것입니다. dma_primetime 검사를 제거하고 AIQ용 전용 프로필을 갖는 것이 계획입니다. 콘솔에 액세스해야 하는 사용자에게는 해당 사용자 프로필이 필요합니다. 하지만 현재는 구현되지 않습니다.

1. Adobe Marketing Cloud 또는 @Peter에서 조직@Eric 온보딩할 수 있습니다.  지금은 &quot;Experience Cloud&quot;라고 부르지만, 그것은 사소한 것입니다.  더 자세한 내용이 있습니까? 다른 그룹에서 관리합니까? 그렇다면 링크, 연락처 등을 제공합니까? 또한 조직이 이미 Experience Cloud의 일부인지 확인하는 것에 대한 경고가 포함되어 있어야 합니다.

2. http://adminconsole.adobe.com/에서 사용자에게 &quot;TVE 대시보드 읽기-쓰기&quot; 또는 &quot;TVE 대시보드 읽기 전용&quot; 프로필이 할당되어 있습니다.
@Eric, 어떻게 하는지 알아?  하위 단계가 있습니까?  고객이 읽기-쓰기와 읽기 전용 을 선택한 이유를 고객에게 설명할 수 있습니까?
@Cristina, 이것이 일시적인 접근이고 아마도 다음 버전에서 어떻게 작동할지 짧은 설명을 제공할 수 있습니까?

3. 조직 id가 AIQ 측 @Cristina에 허용 목록에 추가되어 있다면, 이를 관리하기 위해 적절한 프로세스를 적용할 수 있습니까?  예를 들어 조직의 조직 ID 등이 있는 &quot;DL-AdobePass-Eng AdobePass-Eng@adobe.com&quot;에 이메일을 보낼 수 있습니다.

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

Enterprise Dashboard Adobe에 액세스하면 Adobe Marketing Cloud 조직에 새로 생성된 두 사용자 그룹이 표시됩니다.

TVE 대시보드 읽기-쓰기 - 이 그룹의 구성원은 대시보드 TVE 대시보드 읽기 전용 의 편집 가능한 모든 섹션에 전체 권한을 갖습니다. 이 그룹의 구성원은 전체 대시보드에 대한 보기 권한만 갖습니다. Adobe Enterprise Dashboard에서 TVE 대시보드 읽기-쓰기 사용자 그룹에 계정을 추가한 다음 Adobe Primetime TVE 대시보드에 로그인하십시오.  그런 다음 위에 나열된 두 사용자 그룹에서 사용자를 추가 및 제거하여 Enterprise Dashboard에서 사용자 권한을 관리할 수 있습니다.

...........

제공한 설명서에는 Adobe Pass 콘솔에 적용되는 &quot;Primetime TVE 대시보드 사용자 프로비저닝 시작하기&quot;라는 부분이 있지만 AIQ에도 비슷해야 합니다.
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide AIQ에 관심이 있는 조직은 Adobe Marketing Cloud 조직에 등록된 조직이어야 합니다. 해당 조직의 사용자는 TVE 대시보드 읽기-쓰기 또는 TVE 대시보드 읽기 전용으로 할당되어야 합니다.
기술 자료만 위해 이러한 사용자 그룹은 사용자 계정에 대해 dma_primetime 제품 컨텍스트를 설정합니다. AIQ 코드에서는 액세스를 제공할 때 이 제품 컨텍스트를 확인하고 있습니다. 내부적으로, 코드에서 다음과 같은 추가 조건이 있습니다. 사용자가 데이터에 액세스할 수 있도록 조직 id를 화이트리스트에 추가해야 합니다.
이것이 현재 우리가 가지고 있는 것입니다. dma_primetime 검사를 제거하고 AIQ용 전용 프로필을 갖는 것이 계획입니다. 콘솔에 액세스해야 하는 사용자에게는 해당 사용자 프로필이 필요합니다. 하지만 현재는 구현되지 않습니다.

..........................

1. Adobe Marketing Cloud에서 조직 온보딩
2. http://adminconsole.adobe.com/에서 사용자에게 &quot;TVE 대시보드 읽기-쓰기&quot; 또는 &quot;TVE 대시보드 읽기 전용&quot; 프로필이 할당되어 있습니다.
3. AIQ 측에서 조직 ID를 허용 목록에 추가한 경우
