# Gradle Setting Practice

## Gradle관련 학습 정리
### 1. gradlew, gradlew.bat 차이 

> - Gradle Wrapper의 2가지 버전
> - gradlew는 Unix기반 시스템에서 사용
> - gradlew.bat은 windows 시스템에서 사용

<br/>
<br/>

### 2. plugin 정보가 필요한 이유
Dependency 설정 이외에도 plugin으로 다음과 같이 명시해주는 이유

Plugin은 Gradle Tasks의 집합을 의미

만약 모든 Tasks들을 일일이 명시해준다면 매우 귀찮고 비효율적일 것

따라서 plugin을 활용하면 해당 tasks들을 직접 명시해주지 않아도 사용할 수 있게 된다.

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.0'
    id 'io.spring.dependency-management' version '1.1.4'
}
```
<br/>
<br/>

### 3. tasks.register을 주로 쓰는 이유
task를 등록하는 방법은 크게 2가지가 있는 것 같다.
```groovy
task gretting {
    description = 'print greeting'
    println("hi")
}

--- 

tasks.register('greeting2') {
    description = 'print greeting2'
    print("hihi")
}

```

첫번째 방법 같은 경우 직접 task를 지정해주었는데 이렇게 작성한다면,
해당 task가 gradle스크립트가 로드될 때 즉시 생성되게 된다.

반면, tasks.register을 활용하여 task를 등록하게 될 경우 지연 생성이 된다.
즉 해당 task가 필요로 할 때 까지는 task가 생성되지 않는 것이다.

이는 빌드 성능을 더 상승시키는 효과가 있고, 따라서 많은 수의 테스크가 있는 프로젝트에서는
tasks.register 방식을 선호한다고 한다.