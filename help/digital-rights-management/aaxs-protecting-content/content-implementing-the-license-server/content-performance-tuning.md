---
seo-title: 성능 조정
title: 성능 조정
uuid: bb5321a0-48ef-49cb-aaf0-00d7ab9562fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 성능 조정{#performance-tuning}

다음 팁을 사용하여 성능을 높이십시오.

* 네트워크 HSM을 사용하는 것은 직접 연결된 HSM을 사용하는 것보다 훨씬 느릴 수 있습니다.
* 성능을 향상시키려면 SDK의 &quot;thirdparty/cryptoj&quot; 폴더에 있는 플랫폼별 라이브러리를 배포하여 암호화 작업에 대한 기본 지원을 선택적으로 활성화할 수 있습니다. 기본 지원을 활성화하려면 플랫폼에 대한 라이브러리(Windows의 경우 jsafe.dll 또는 Linux의 경우 libjsafe.so)를 경로에 추가하십시오.

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >동일한 Tomcat 인스턴스에서 여러 웹 응용 프로그램을 실행하고 경로에 `jsafe.dll` 있는 경우 로드되는 첫 번째 웹 응용 프로그램만 `jsafe.dll` 라이브러리를 로드할 수 있습니다. 따라서 첫 번째 웹 애플리케이션만이 기본 지원을 활용할 수 있습니다. 이러한 경우 모든 웹 애플리케이션의 성능을 향상시키려면 WAR 파일 `cryptoj.jar`외부에 배치합니다. 예를 들어, `<tomcat_installation_folder>/lib` 디렉토리에 있습니다.

* 64비트 버전의 Red Hat® 또는 Windows와 같은 64비트 운영 체제는 32비트 운영 체제보다 훨씬 향상된 성능을 제공합니다.

