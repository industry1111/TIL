## Spring Annotation
****

### @CreatedDate
- Entity가 생성되어 저장될 때 시간이 자동 저장됩니다.

### @EnableJpaAuditing
- JPA Auditing 활성화
- application 클래스에 추가
```java
@EnableJpaAuditing
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

### @GetMappring
- @GetMapping은(`name`) `name`이란 주소로 이동하게 해줍니다.
- Get 요청을 받을 수 있는 API를 만들어 줍니다.
- `http://localhost:8080/hello`  요청이 오면 문자열 hello를 반환하는 기능을 가지게 됩니다.
```java
@GetMapping("/hello")
public String hello() {
    return "hello";
}
```

### @LastModifiedDate
- 조회한 Entity의 값을 변경할 때 시간이 자동 저장됩니다.
- 
### PathVariable
- RESTful API에서 경로의 일부를 변수로 사용하기 위해 사용. 
- 경로의 일부를 변수로 바인딩하여 컨트롤러 메서드에서 사용할 수 있도록 합니다.
```java
@GetMapping("/hello/{id}")
public ResponseEntity<User> hello(@PathVariable int id) {
        // 사용자 ID에 해당하는 정보를 조회하는 로직
        User user = userService.getUserById(id);
        if (user != null) {
        return ResponseEntity.ok(user);
        } else {
        return ResponseEntity.notFound().build();
        }
}
```

### @RequestBody
- JSON으로 넘어온 데이터를 객체로 매핑해주는 어노테이션입니다.


### `@RestController`
- 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줍니다.
- 예전에는 @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해줍니다.
```java
@RestController
public class HelloController {...}
```

### @Transactinal
- 메소드 내에서 트랜잭션 범위를 설정하고 관리 할 수 있두록 지원
```java
import org.springframework.transaction.annotation.Transactional;

@Transactional(isolation = Isolation.READ_COMMITTED, propagation = Propagation.REQUIRED, 
        readOnly = false, timeout = 60, rollbackFor = {SQLException.class}, noRollbackFor = {NullPointerException.class})
public void performDatabaseOperation() {
    // 데이터베이스 작업 수행
}
```
****
## Test Annotation
*****

### @@ExtendWith(SpringExtension.class)
- 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킵니다.

### @LocalServerPort
- 랜덤으로 새로운 포트를 생성하여 테스트를 진행합니다.
```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class MyIntegrationTest {

    @LocalServerPort
    private int serverPort;

    @Test
    public void testServerPort() {
      ...
    }
}

```

### @WebMvcTest
- 여러 스프링 어노테이션 중, Web(Spring MVC)에 집중할 수 있는 어노테이션입니다.
- 선언할 경우 `@Controller`, `@ControllerAdvice` 등을 사용할 수 있습니다.
- 단, `@Service`, `@Component`, `@Repository` 등은 사용할 수 없습니다.
  - **private MockMvc mvc**
    - URL 및 HTTP 메서드를 이용한 테스트가 가능
    - 응답의 상태, 헤더, 본문을 검증 할 수 있음
```java
...
//MockMvc에 사용된 패키지
import org.springframework.test.web.servlet.MockMvc;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@ExtendWith(SpringExtension.class)
@WebMvcTest(controllers = HelloController.class)
public class HelloControllerTest {
    
    @Autowired
    private MockMvc mvc;
    
    @Test
    public void hello가_리턴된다() throws Exception {
        String hello = "hello";
        
        mvc.perform(get("/hello"))                      //get("/hello")로 HTTP GET 요청
                .andExpect(status().isOk())             //응답 상태코드가 200인지 확인
                .andExpect(content().string(hello));    //응답 바디 내용이 hello인지 확인
    }
}
```

### @AfterEach, @BeforeEach
- `@AfterEach` : 단위 테스트가 끝날 때마다 수행되는 메소드를 지정
- `@BeforeEach` : 단위 테스트가 시작되기 전에 수행되는 메소드를 지정


### @BeforeAll, @AfterAll

- 모든 테스트 메소드가 실행전(`@BeforeAll`) 후(`@AfterAll`) 한번 실행된다.
- 보통은 **배포 전 전체 테스트를 수행할 때** 테스트 간 데이터 침범을 막기 위해 사용하며,
- static 메소드로 선언하거나 ,'@TestInstance(TestInstance.Lifecycle.PER_CLASS)'를 클래스에 선언해야한다.

```java
@TestInstance(TestInstance.Lifecycle.PER_CLASS)
@ExtendWith(SpringExtension.class)e
@SpringBootTest
public class HelloControllerTest {
    @BeforeAll
    public void setUp() {
        System.out.println("BeforeAll");
    }
    
    @AfterAll
    public void tearDown() {
        System.out.println("AfterAll");
    }
}
```


****
## Lombok
****
- `@Getter` : 선언된 모든 필들의 get 메소드를 생성
- `@RequiredArgsConstructor` : 선언된 모든 final 필드가 포함된 생성자를 생성
- `@NoArgsConstructor` : 파라미터가 없는 기본 생성자를 생성
- `@Builder` : 해당 클래스의 빌더 패턴 클래스를 생성, 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함


****
## JPA Annotation
****

### `@Column`
- 컬럼매핑
- name = ""(default): 매핑할 테이블의 컬럼이름(객체의 필드이름),
- insertable/updatable : 등록 변경 가능여부 (TRUE) - DB에 컬럼 반영여부
- nullable(DDL) : null 값 허용 여부(TRUE)  false 설정 시 NOT NULL 제약조건 생성
- unique(DDL) : @Table(uniqueConstrains와 같음 )
- columnDefinition(DDL) : 데이터베이스 컬럼 정보를 직접 줄 수 있다.
- length(DDL) :  문자길이 제약 조건 String  타입에만 서용 (255)
- precision/scale : BigDecimal/BigInteger 타입에서 사용 precision 은 소수점 포함 전체자릿수, scale 은 소수점 자릿수

### `@Entity`

### `@Enumerated`
- enum 타입 매핑
- 
### `@GeneratedValue`
- PK의 생성 방법을 매핑하는 애노테이션
  - strategy = GenerationType.AUTO : 방언에 따라 자동 지정, 기본
  - IDENTITY : 데이터베이스에 위임
  - SEQUENCE : 데이터베이스 시퀀스 오브젝트 사용 , ORACLE @SequenceGenerator 필요
  - TABLE :

### `@Id`
- PK 매핑

### `@Lob`
- BLOB,CLOB 매핑

### `@Temporal`
- 날짜타입 매핑
- LocalDate, LocalDateTime 사용할 때는 생략 가능

### `@Transient`
- 특정 필드를 컬럼에 매핑하지 않음 (매핑 무시)