---
seo-title: 사용자 정의 DRM 정책 만들기(선택 사항)
title: 사용자 정의 DRM 정책 만들기(선택 사항)
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 사용자 정의 DRM 정책 만들기(선택 사항){#create-custom-drm-policies-optional}

Primetime Cloud DRM 보호 키트에는 패키징 중에 사용할 수 있는 몇 가지 미리 구성된 정책이 포함되어 있습니다. 예를 들어 특정 SWF 허용 목록 권한과 같은 추가 정책 구성을 원하는 경우 포함된 Primetime DRM 정책 관리자를 사용하여 사용자 지정 정책을 생성할 수 있습니다.

>[!NOTE]
>
>모든 정책은 사용자 지정 인증/권한 부여 워크플로우의 사용 여부와 관계없이 익명 인증(사용자 이름 암호 또는 사용자 지정 아님)을 사용해야 합니다.

Policy Manager에 포함된 [!DNL flashaccesstools.properties] 구성 파일은 Primetime Cloud DRM 서비스가 지원하는 구성 가능한 정책 옵션만 표시하도록 수정되었습니다. Primetime Cloud DRM 서비스에서 지원되지 않는 정책 옵션을 설정하면 라이선스 획득 오류가 발생합니다. Primetime DRM 정책 관리자 사용에 대한 자세한 내용은 다음을 참조하십시오. [Primetime DRM 참조 구현: 정책 관리자](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

새 정책을 만들려면 원하는 대로 [!DNL flashaccesstools.properties] 파일을 업데이트한 다음 명령을 사용합니다.

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 사용자 정의 인증/권한 부여에 대한 정책을 동적으로 만들기{#create-policies-dynamically-for-custom-auth-entitlement}

Primetime Cloud DRM 사용자 정의 인증/자격 부여를 사용하고 있고 각 라이선스 요청에 대한 새로운 DRM 정책을 동적으로 만들려면(사전 생성된 풀에서 정책을 가져오는 대신) Adobe에서 직접 Primetime DRM Java SDK를 사용하는 것이 좋습니다. Java SDK를 직접 사용하는 것이 정책 파일을 디스크에 자동으로 출력하여 디스크 I/O 오버헤드를 발생시키는 [!DNL AdobePolicyManager.jar] 도구보다 빠릅니다.

Java SDK를 사용하는 샘플 코드는 and라는 [!DNL /Primetime DRM PolicyManager/sampleCode/] 디렉토리에서 찾을 수 [!DNL CreatePolicy.java] 있습니다 [!DNL CreatePolicyWithOutputProtection.java]. Java SDK에 대한 JavaOcs 및 설명서는 Adobe Primetime DRM SDK의 [개요에서 확인할 수 있습니다.](../../../digital-rights-management/drm-sdk-overview/overview.md)

샘플을 빌드하고 실행하려면 .java 파일을 ../libs/ 폴더에 복사하여 다음을 실행하십시오.

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
