# MockWebServer

## MockWebServer란?
- Square사에서 만들었으며, 테스트를 위한 가짜 서버를 만들어서 테스트를 진행할 수 있음
- Spring Team에서는 MockWebServer를 사용하여 테스트를 하라고 권장한다고 한다.

## MockWebServer 사용법

### 의존성 추가
```Gradle
testImplementation 'com.squareup.okhttp3:mockwebserver'
```

### 테스트 코드에 MockWebServer를 추가
```java
//...
import okhttp3.mockwebserver.MockResponse;

@ExtendWith(SpringExtension.class)
@SpringBootTest(webEnvironment =
        SpringBootTest.WebEnvironment.RANDOM_PORT)
public class PostsApiControllerTest {
    
    public static MockWebServer mockWebServer;

    @BeforeAll
    static void setUp() throws IOException {
        mockWebServer = new MockWebServer();
        mockWebServer.start();
    }
    
    @BeforeEach
    void initialize() {
        final String baseUrl = String.format("http://localhost:%s", mockWebServer.getPort());
        final WebClient webClient = WebClient.create(baseUrl);
        
    }
    
    @AfterAll
    static void tearDown() throws IOException {
        mockWebServer.shutdown();
    }
    
    @Test
    class MockWebServerTest {
        
    }
}
```

### Reference
[baeldung](https://www.baeldung.com/spring-mock-web-server)
