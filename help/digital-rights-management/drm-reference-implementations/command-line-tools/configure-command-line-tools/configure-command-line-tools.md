---
seo-title: 명령줄 도구 구성 및 실행
title: 명령줄 도구 구성 및 실행
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 명령줄 도구 {#configure-and-run-the-command-line-tools} 구성 및 실행

명령줄 도구에는 도구를 실행하기 전에 [!DNL flashaccesstools.properties] *에서 값을 설정해야 하는 관련 속성이 있습니다.* 일부 명령줄 도구에서는 명령줄에서 속성 값을 지정할 수도 있습니다. 명령줄에서 지정하는 값은 [!DNL flashaccesstools.properties]에서 제공하는 값보다 우선합니다.

사용할 명령줄 도구를 활성화하려면 [!DNL flashaccesstools.properties]의 다음 섹션에서 설정을 수정해야 합니다.

* **Media Packager 속성**   [!DNL AdobePackager.jar] - (용)

* **정책 업데이트 목록 관리자 및 해지 목록 관리자 속성**  - (및 [!DNL AdobePolicyUpdateListManager.jar] 에  [!DNL AdobeRevocationListManager.jar])

* **정책 관리자 속성**  - (용)  [!DNL AdobePolicyManager.jar]

* **라이선스 생성기 속성**   [!DNL AdobeLicenseGenerator.jar] - (용)