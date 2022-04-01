---
description: 빌드 자동화 툴을 이용하면 컴파일, 라이브러리 다운로드, 패키징, 테스팅 등을 자동화할 수 있다.
---

# 빌드 자동화 툴 : Gradle / Library

### 빌드 자동화를 사용하는 이유

* 모든 자동화의 시작은 반복 작업에서 시작된다.
*   빌드 순서 고려

    ex. **빌드 → 유닛 테스트 실행** 작업
* 개발자가 모든 라이브러리를 컴파일해 빌드를 하고 유닛 테스트를 실행시키는 작업 필요
  * 베포할 때마다 반복 → 인적 자원 낭비

**빌드 자동화 툴이 없다면?**

* 라이브러리 사용을 위해 사이트에서 jar 파일을 다운로드 받고,
* IDE에 라이브러리를 추가

필요한 라이브러리 개수만큼 jar파일을 다운받는 반복.. 또 반복...

## Grade (http://gradle.org/)

***

Java, Groovy, Scala 등 JVM에서 실행되는 언어의 빌드 자동화를 위해 사용된다.

* Groovy언어로 작성됨.

**작성 예시**

```groovy
plugins {
	id 'org.springframework.boot' version '2.6.6'
	id 'io.spring.dependency-management' version '1.0.11.RELEASE'
	id 'java'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'

configurations {
	compileOnly {
		extendsFrom annotationProcessor
	}
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	compileOnly 'org.projectlombok:lombok'
	runtimeOnly 'com.h2database:h2'
	annotationProcessor 'org.projectlombok:lombok'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

tasks.named('test') {
	useJUnitPlatform()
}
```

### plugins

공식 웹 사이트에 따르면 그레이들은 의도적으로 많은 기능을 제공하지 않는다.

→ 대신 플러그인을 통해 그레이들을 확장하여 사용할 수 있다!

ex. `Java`

* 자바를 컴파일하려면 그레이들 자바 플러그인이 필요
*   id ‘ java’

    : 빌드를 위해 자바 플러그인을 사용함을 명시

`org.springframework.boot` or `io.spring.dependency-management`도 마찬가지

* 이 플러그인을 사용하려면 버전 정보를 넘겨주어야 함



### group, version, sourceCompatibility

프로젝트의 메타데이터다.

**group**

: artifact(애플리케이션) 배포시 사용

* Spring Initializr의 Project Metadata에서 정의한 Group과 동일

**version**

: 프로젝트의 버전

* 이상적으로 프로덕션 배포마다 버전이 올라감
* 버전을 어떻게 올리는지는 프로젝트마다 다름

**sourceCompatibility**

*   java 컴파일을 위해 java 플러그인 추가

    → 자바 플러그인은 sourceCompatibility에 명시된 자바 버전을 이용해 소스 컴파일



### **Lombok**

개발 시간 단축을위해 롬복 라이브러리를 사용한다.

* 어노테이션을 추가하면 컴파일 시 그에 상용하는 코드를 만들어주는 라이브러리
* 롬복이 코드를 작성하려면 **‘어노테이션 프로세서’가 필요**

bulid.grade 코드를 보면 configurations와 dependencies에 명시함을 볼 수 있다.



### Repository

: 그레이들이 라이브러리를 다운로드하는 곳

* mavenCentral을 주로 사용

### Dependency

프로젝트에서 사용할 라이브러리를 명시하면 그레이들이 리포지터리에서 라이브러리를 다운 및 설치한다.

* implementation, runtimeOnly 등 : 라이브러리의 scope에 대한 내용

### Test

그레이들을 사용하면 빌드뿐만 아니라 **유닛 테스트도 실행시킬 수 있다.**
