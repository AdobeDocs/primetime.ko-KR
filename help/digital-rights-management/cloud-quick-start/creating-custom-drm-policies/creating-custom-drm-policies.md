---
title: 사용자 정의 DRM 정책 생성(선택 사항)
description: 사용자 정의 DRM 정책 생성(선택 사항)
copied-description: true
exl-id: a74f60b1-96a0-4fc4-bbf2-5db78f343562
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 사용자 정의 DRM 정책 생성(선택 사항){#create-custom-drm-policies-optional}

Primetime Cloud DRM 보호 키트는 패키징 중에 사용할 수 있는 사전 구성된 몇 가지 정책과 함께 제공됩니다. 특정 SWF 허용 목록 권한 등 추가 정책 구성이 필요한 경우 포함된 Primetime DRM 정책 관리자를 사용하여 사용자 지정 정책을 생성할 수 있습니다.

>[!NOTE]
>
>사용자 지정 인증/자격 워크플로우의 사용 여부와 관계없이 모든 정책은 익명 인증(사용자 이름 암호 또는 사용자 지정 아님)을 사용해야 합니다.

정책 관리자에는 다음 항목이 포함됩니다. [!DNL flashaccesstools.properties] Primetime Cloud DRM 서비스가 지원하는 구성 가능한 정책 옵션만 표시하도록 수정된 구성 파일. Primetime Cloud DRM 서비스에서 지원하지 않는 정책 옵션을 설정하면 라이선스 획득 오류가 발생합니다. Primetime DRM 정책 관리자 사용에 대한 자세한 내용은 다음을 참조하십시오. [Primetime DRM 참조 구현: 정책 관리자](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

새 정책을 만들려면 [!DNL flashaccesstools.properties] 원하는 대로 파일을 만든 다음 명령을 사용합니다.

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 사용자 지정 인증/권한 부여에 대해 동적으로 정책 만들기{#create-policies-dynamically-for-custom-auth-entitlement}

Primetime Cloud DRM 사용자 지정 인증/권한 부여를 사용 중이며 각 라이선스 요청에 대해 사전 생성된 풀에서 정책을 가져오는 대신 새 DRM 정책을 동적으로 생성하려는 경우, Adobe은 Primetime DRM Java SDK를 직접 사용할 것을 권장합니다. Java SDK를 직접 사용하는 것이 [!DNL AdobePolicyManager.jar] 정책 파일을 디스크에 자동으로 출력함으로써 디스크 I/O 오버헤드가 발생합니다.

Java SDK를 사용하는 샘플 코드는에서 찾을 수 있습니다. [!DNL /Primetime DRM PolicyManager/sampleCode/] 디렉토리, 이름 [!DNL CreatePolicy.java] 및 [!DNL CreatePolicyWithOutputProtection.java]. Java SDK에 대한 JavaDoc 및 설명서는 [Adobe Primetime DRM SDK 개요](../../../digital-rights-management/drm-sdk-overview/overview.md)

샘플을 빌드하고 실행하려면 .java 파일을 ../libs/ 폴더에 복사하고 다음을 실행하십시오.

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
