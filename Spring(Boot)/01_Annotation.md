## Controller Annotation
****

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

### `@RestController`
- 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줍니다.
- 예전에는 @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해줍니다.
```java
@RestController
public class HelloController {...}
```


# Test Annotation
****

### @@ExtendWith(SpringExtension.class)
- 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킵니다.
- 여기서는 SpringExtension이라는 스프링 실행자를 사용합니다.

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



## Lombok
- `@Getter` : 선언된 모든 필들의 get 메소드를 생성
- `@RequiredArgsConstructor` : 선언된 모든 final 필드가 포함된 생성자를 생성
- `@NoArgsConstructor` : 파라미터가 없는 기본 생성자를 생성
- `@Builder` : 해당 클래스의 빌더 패턴 클래스를 생성, 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함



