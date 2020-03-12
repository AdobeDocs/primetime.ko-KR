---
seo-title: 크로스 도메인 DRM 정책 파일
title: 크로스 도메인 DRM 정책 파일
uuid: cb91a85a-1825-4fd7-a25c-880cdbd5c8b8
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 크로스 도메인 DRM 정책 파일 {#crossdomain-drm-policy-file}

라이센스 서버가 비디오 재생 SWF가 아닌 다른 도메인에 호스팅되는 경우 SWF가 라이센스 서버에서 라이센스를 요청하도록 하는 크로스 도메인 DRM 정책 파일( [!DNL crossdomain.xml])이 필요합니다. 크로스 도메인 DRM 정책 파일은 XML 파일로 표현되므로 서버에서 다른 도메인에서 제공되는 SWF 파일에 데이터와 문서를 사용할 수 있음을 나타냅니다. 라이선스 서버의 크로스 도메인 DRM 정책 파일에 지정된 도메인에서 제공되는 모든 SWF 파일은 해당 라이선스 서버의 데이터 또는 에셋에 액세스할 수 있습니다.

Adobe에서는 개발자가 트러스트된 도메인만 라이센스 서버에 액세스하고 웹 서버의 라이센스 하위 디렉토리에 대한 액세스를 제한하여 크로스 도메인 정책 파일을 배포할 때 모범 사례를 따를 것을 권장합니다.

크로스 도메인 DRM 정책 파일에 대한 자세한 내용은 다음 위치를 참조하십시오.

* 웹 사이트 컨트롤(DRM 정책 파일)
* 크로스 도메인 DRM 정책 파일 사양: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

