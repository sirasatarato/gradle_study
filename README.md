# Gradle
> 안드로이드 애플리케이션은 그레이들 빌드 시스템으로 빌드합니다. 그레이들은 쉽게 사용자 정의를 할 수 있는 최신 API를 제공하며 자바 진영에서 널리 사용합니다.

## 구조
> 안드로이드: 멀티 프로젝트 구조  
> Project Stucture창으로 속성 값들을 시각적으로 표현 가능
- setting.gradle: 하위 프로젝트(이하 모듈)을 포함하는 파일
- 프로젝트 build.gradle: 
  - buildscript: 안드로이드 플러그인을 버전을 몇으로 할지 어디서 다운받을지 지정
    - repositories: 기본값(jcenter), 다른 저장소도 가능(주로 mavenCentral)
    - dependencies
  - allprojects: 최상위 프로젝트와 하위 모듈이 공통적으로 사용할 내용을 지정
    - repositories: 기본값(jcenter)
  - 사용자 정의 테스크: 기본(clean: 루프 프로젝트와 하위 모듈의 build 디렉터리를 제거, type: Delete부분은 내장 테스크인 Delete를 상속받겠다는 의미)
- 모듈 build.gradle: 
> 그레이들 플러그인은 안드로이드 환경을 위한 DSL(도메인 특화 언어)를 구현했다.
  - apply: 안드로이드 플러그인을 지정
  - android: 프로젝트 세부 내용 정의
    - compileSdkVersion: 컴파일 SDK 버전
    - BuildToolVersion: 빌드 툴 버전
    - defaultConfig: 아래 속성들 지정
      - appllicationId: 애플리케이션 패키지 이름 정의, 우선순위가 높으며 구글플레이 스토어에서 유일한 이름으로 정의된다.
      - minSdkVersion: 지원하는 최소 SDK버전, 이 값보다 낮은 기기는 해당 애플리케이션을 검색, 설치조차 할 수 없다.
      - targetSdkVersion: 애플리케이션이 의도하는 SDK버전
      - versionCode: 애플리케이션의 버전을 나타내는 정수값
      - versionName: 사용자에게 배포되는 애플리케이션 버전을 나타내는 문자열
  - dependencies:
    - compile fileTree(dir: 'libs', include: ['*.jar']): libs 디렉터리 안에 있는 모든 jar 파일들을 참조
    - testCompile 'junit:junit4.12': junit:junit4.12을 다운받고 안드로이드 API에 연관되지 않는 로컬 유닛 테스트를 위한 /src/androidTest/java 디렉터리에 참조
