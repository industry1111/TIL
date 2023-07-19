## JWT (JSON Web Token)
- JWT는 유저를 인증하고 식별하기 위한 토큰 기반 인증이다.  토큰은 세션과는 달리 서버가 아닌 `클라이언트에 저장`되기 때문에 메모리나 스토리지 등을 통해 세션을 관리 했던 서버의 부담을 덜 수 있다.
  핵심적인 특징이 있다면, 토큰 자체에 사용자의 권한 정보나 서비스를 사용하기 위한 정보가 포함 된다는 것이다.
- JWT를 사용하면 RESTful과 같은 `무상태(Stateless)`인 환경에서 사용자 데이터를 주고 받을 수 있게 된다.
- JWT는 `Base64 URL-safe Encode`를 통해 인코딩하여 직렬화한 것이 포함되며, 토큰 내부에는 위변조 방지를 위해 개인크를 통한 `전자서명`도 있다

#### JWT 진행 방식
1. 클라이언트 사용자가 아이디, 패스워드를 통해 웹서비스 인증
2. 서버에서 `서명된(Signed)` JWT를 생성하여 클라이언트에 응답으로 돌려주기
3. 클라이언트가 서버에 데이터를 추가적으로 요구할 때 JWT를 HTTP Header에 첨부
4. 서버에서 클라이언트로 부터 온 JWT를 검증
5. 일치한다면 인증을 허용, 일치하지 않는다면 인증이 실패

#### JWT 구조
- Header
    - JWT에서 사용할 타입과 해시 알고리즘의 종류가 담겨있다.
      ```json
      {
         "alg" : "HS256", // HS256는 이 토큰이 HMAC-SHA256를 사용하여 서명됨을 의미
         "typ" : "JWT"
      }
      ```
- Payload
    - 서버에서 첨부한 사용자 권한 정보와 데이터가 담겨있다.
  ```json
    {
      "loggedInAs" : "admin", // 사용자 지정 클레임(loggedInAs)을 의미
      "iat" : 1422779638      // 표준 Issued At Time 클레임(iat) 의미 
    }
    ```
- Signature
    - Header, Payload를 `Base64 URL-safe Encode`를 한 인후 Header에 명시된 해시함수를 적용하고, `개인키(Private Key)`로 서명한 전자서명이 담겨있다
      ```json
          HMAC-SHA256(                        //서명은 Base64url 인코딩을 이용하여 헤더와 페이로드를 인코딩하고 이 둘을 점(.) 구분자로 함께 연결시킴으로써 계산
            secret,
            base64urlEncoding(header) + '.' +
            base64urlEncoding(payload)
          )
      ```

### SpringSecurity + JWT 구현

#### build.gradle 설정
```groovy
dependencies {
    //JJWT
    implementation("io.jsonwebtoken:jjwt-api:0.11.5")
    runtimeOnly("io.jsonwebtoken:jjwt-impl:0.11.5")
    runtimeOnly("io.jsonwebtoken:jjwt-jackson:0.11.5")
}
```
#### 샘플 코드

```java
public class JavaJJWTTest {

    String secretKey = "SecretKeyToGenJWTsSecretKeyToGenJWTsSecretKeyToGenJWTs";

    private void printToken(String token) {
        System.out.println("token: " + token);
        System.out.println("header: " + decodeToken(token.split("\\.")[0]));
        System.out.println("payload: " + decodeToken(token.split("\\.")[1]));
    }

    private String decodeToken(String token) {
        return new String(Base64.getDecoder().decode(token));
    }

    @Test
    void test_okta_token() {
        Map<String, Object> claims = new HashMap<>();
        claims.put("sub", "test");
        claims.put("name", "rhgudrb");
        claims.put("admin", "true");
        claims.put("exp", Instant.now().plusSeconds(60*60*24).getEpochSecond());
        claims.put("iat", Instant.now().getEpochSecond());

        String oktaToken = Jwts.builder()
                .addClaims(claims)
                .signWith(Keys.hmacShaKeyFor(secretKey.getBytes()), SignatureAlgorithm.HS256)
                .compact();
        printToken(oktaToken);

        Jws<Claims> claimsJws = Jwts.parserBuilder()
                .setSigningKey(Keys.hmacShaKeyFor(secretKey.getBytes()))
                .build()
                .parseClaimsJws(oktaToken);
        System.out.println("claimsJws: " + claimsJws);
    }

}
```
#### JWT 토큰을 생성하고 검증하는 JwtUtils 클래스

```bash
echo asdasdasdaskdhafguiqqd | base64

YXNkYXNkYXNkYXNrZGhhZmd1aXFxZAo=
```

```java

@Component
@RequiredArgsConstructor
@Slf4j
public class JwtTokenProvider {
    private final PrincipalDetailsService principalDetailsService;

    @Value("${jwt.token.key}")
    private String secretKey;

    //토큰 유효시간 설정
    private Long tokenValidTime = 240 * 60 * 1000L;

    //secretkey를 미리 인코딩 해줌.
    @PostConstruct
    protected void init() {
        secretKey = Base64.getEncoder().encodeToString(secretKey.getBytes());
    }

    //JWT 토큰 생성
    public String createToken(String email, String provider) {

        //payload 설정
        //registered claims
        Date now = new Date();
        Claims claims = Jwts.claims()
                .setSubject("access_token") //토큰제목
                .setIssuedAt(now) //발행시간
                .setExpiration(new Date(now.getTime() + tokenValidTime)); // 토큰 만료기한

        //private claims
        claims.put("email", email); // 정보는 key - value 쌍으로 저장.
        claims.put("provider", provider);

        return Jwts.builder()
                .setHeaderParam("typ", "JWT") //헤더
                .setClaims(claims) // 페이로드
                .signWith(SignatureAlgorithm.HS256, secretKey)  // 서명. 사용할 암호화 알고리즘과 signature 에 들어갈 secretKey 세팅
                .compact();
    }

    //JWT 토큰에서 인증정보 조회
    public Authentication getAuthentication(String token) {
        UserDetails userDetails = principalDetailsService.loadUserByUsername(this.getUserPk(token));
        return new UsernamePasswordAuthenticationToken(userDetails, "", userDetails.getAuthorities());
    }

    // 토큰에서 회원 정보 추출
    public String getUserPk(String token) {
        return (String) Jwts.parser().setSigningKey(secretKey).parseClaimsJws(token).getBody().get("email");
    }

    // Request의 Cookie에서 token 값을 가져옵니다. "Authorization" : "TOKEN값'
    public String resolveToken(HttpServletRequest request) {
        Cookie jwtCookie = WebUtils.getCookie(request, "JWT");

        if (jwtCookie != null) {
            return jwtCookie.getValue();
        }
        return null;
    }

    // 토큰의 유효성 + 만료일자 확인  // -> 토큰이 expire되지 않았는지 True/False로 반환해줌.
    public boolean validateToken(String jwtToken) {
        try {
            Claims claims = Jwts.parser().setSigningKey(secretKey).parseClaimsJws(jwtToken).getBody();

            return !claims.getExpiration().before(new Date());
        } catch (Exception e) {
            return false;
        }
    }
}
```

| 참고 자료

[https://pronist.dev/](https://pronist.dev/143)
