### build.gradle 설정
```gradle
    //소셜로그인 등 클라이언트입장에서 소셜 기능 구현시 필요한 의존성
    implementation 'org.springframework.boot:spring-boot-starter-oauth2-client'
    implementation('org.springframework.boot:spring-boot-starter-security')
```


### SecurityConfig.java 파일을 작성
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.util.matcher.AntPathRequestMatcher;

@Configuration
@EnableWebSecurity
public class SecurityConfig {
@Bean
SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
http.authorizeHttpRequests().requestMatchers(
new AntPathRequestMatcher("/**")).permitAll()
;
return http.build();
}
}
```