

# Maven(메이븐)과 Gradle(그래들) 관련 질문

## 🚀 Maven과 Gradle이 뭐야?

Maven(메이븐)과 Gradle(그래들)은 **빌드 도구(Build Tool)** 입니다. 프로젝트의 라이브러리를 관리하고, 빌드하고, 실행하고, 배포하는 역할을 합니다.

Spring 프로젝트에서 `spring-boot-starter-web` 같은 라이브러리를 추가할 때 Maven은 `pom.xml`, Gradle은 `build.gradle` 파일을 사용해서 자동으로 다운로드해 줍니다.

즉, "내 프로젝트가 필요한 라이브러리를 쉽게 설치하고, 관리하게 해주는 도구"라고 생각하면 됩니다.

## 📌 왜 필요해?

과거에는 JSP, Servlet 프로젝트를 할 때 필요한 라이브러리를 직접 JAR 파일로 다운로드하고 수동으로 추가해야 했습니다. 하지만 Maven과 Gradle을 사용하면 한 줄로 쉽게 추가할 수 있습니다! 🎉

### 🔹 예전 방식 (불편함 😩)
1. `mysql-connector.jar` 같은 라이브러리를 찾아서 다운로드
2. `WEB-INF/lib/` 폴더에 넣기
3. 다른 버전이 필요하면 다시 다운로드

### 🔹 Maven/Gradle 방식 (편리함 😆)
✅ **Maven (pom.xml에 추가)**

```xml
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.33</version>
    </dependency>
</dependencies>
```

✅ **Gradle (build.gradle에 추가)**

```gradle
dependencies {
    implementation 'mysql:mysql-connector-java:8.0.33'
}
```

👉 이렇게 작성하고 `mvn install` 또는 `gradle build`만 실행하면 자동 다운로드 끝!

## 🔥 Maven vs Gradle 차이점

| 비교 항목 | Maven (메이븐) | Gradle (그래들) |
|-----------|---------------|-----------------|
| 설정 파일 | pom.xml (XML 형식) | build.gradle (Groovy/Kotlin) |
| 속도 | 비교적 느림 | 빠름 (병렬 빌드 지원) |
| 가독성 | XML이라 길고 복잡할 수 있음 | 코드 스타일이라 가독성 좋음 |
| 사용성 | Spring 프로젝트에서 많이 사용됨 | Spring Boot에서 기본 사용 |

### 결론: Spring Boot에서는 Gradle을 더 많이 사용!
👉 하지만 Spring Framework에서는 Maven도 많이 사용됩니다!

## 📌 어떤 걸 배워야 할까?

✅ **Spring Boot를 한다면?**
👉 **Gradle 추천!** (`build.gradle`)

✅ **Spring + Legacy(옛날 프로젝트)를 다뤄야 한다면?**
👉 **Maven도 배워두는 게 좋음!** (`pom.xml`)

## 🛠 Maven/Gradle 명령어 정리

| 명령어 | Maven | Gradle |
|--------|-------|--------|
| 프로젝트 빌드 | `mvn clean install` | `gradle build` |
| 프로젝트 실행 | `mvn spring-boot:run` | `./gradlew bootRun` |
| 라이브러리 업데이트 | `mvn clean package` | `gradle clean build` |

## 🏁 정리하면?

- Maven과 Gradle은 **라이브러리 관리 + 빌드 도구**
- **Spring Boot는 Gradle 기본 사용 (`build.gradle`)**
- **Spring Framework는 Maven도 많이 사용 (`pom.xml`)**
- 기본적인 명령어만 익히면 라이브러리 설치가 편리해짐!

이해됐나요? 추가 질문 있으면 얼마든지 물어봐 주세요~ 😊
