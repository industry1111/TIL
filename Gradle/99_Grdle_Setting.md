### finished with non-zero exit value 1

* InteliJ에서 Gradle 프로젝트를 빌드하려고 할 때, 위와 같은 에러가 발생한다면, 아래와 같이 해결할 수 있다.
* `File` > `Settings` > `Build, Execution, Deployment` > `Build Tools` > `Gradle` 
* `Build and run using` , `Run tests using`을  `InteliJ IDEA`로 변경한다.
![01_Intelij_gradle_non-zero.png](img%2F01_Intelij_gradle_non-zero.png)

### SpringBoot 3.x gradle build error

* SpringBoot 3.x 버전부터는 **자바 17이상**만 지원한다.
* 자바 17이상을 사용하고 있지 않다면, 아래와 같은 에러가 발생한다.
```
 A problem occurred configuring root project 'book'.
> Could not resolve all files for configuration ':classpath'.
   > Could not resolve org.springframework.boot:spring-boot-gradle-plugin:3.1.0.
     Required by:
         project : > org.springframework.boot:org.springframework.boot.gradle.plugin:3.1.0
      > No matching variant of org.springframework.boot:spring-boot-gradle-plugin:3.1.0 was found. The consumer was configured to find a runtime of a library compatible with Java 11, packaged as a jar, and its dependencies declared externally, as well as attribute 'org.gradle.plugin.api-version' with value '7.6.1' but:
          - Variant 'apiElements' capability org.springframework.boot:spring-boot-gradle-plugin:3.1.0 declares a library, packaged as a jar, and its dependencies declared externally:
              - Incompatible because this component declares an API of a component compatible with Java 17 and the consumer needed a runtime of a component compatible with Java 11
              - Other compatible attribute:
                  - Doesn't say anything about org.gradle.plugin.api-version (required '7.6.1')
          - Variant 'javadocElements' capability org.springframework.boot:spring-boot-gradle-plugin:3.1.0 declares a runtime of a component, and its dependencies declared externally:
              - Incompatible because this component declares documentation and the consumer needed a library
              - Other compatible attributes:
                  - Doesn't say anything about its target Java version (required compatibility with Java 11)
                  - Doesn't say anything about its elements (required them packaged as a jar)
                  - Doesn't say anything about org.gradle.plugin.api-version (required '7.6.1')
...

