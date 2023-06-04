# Junit
****

## Assertions란?
- 테스트 코드에서 예상한 값과 실제 값을 비교하여 테스트 결과를 판별하는 것
- Junit에서 제공하는 Assertions 클래스를 사용하여 테스트 코드를 작성할 수 있다.
    - `assertThat()` : 검증하고 싶은 대상을 메소드 인자로 받으며 메소드 체이닝 지원되어 `isEqualTo()`와 같은 메소드를 이어서 사용할 수 있다.
```java
@Test
public void test() {
    String str = "test";
    assertThat(str).isEqualTo("test");
}
```

- `jsonPath` : JSON 응답값을 필드별로 검증할 수 있는 메소드
  - `$`를 기준으로 필드명을 명시한다.
  - 여기서는 `name`과 `amount`를 검증하니 `$.name`, `$.amount`로 검증한다.

```java
@Test
void helloDto가_리턴된다() throws Exception {
        String name = "hello";
        int amount = 1000;

        mvc.perform(get("/hello/dto")
                .param("name", name)
                .param("amount", String.valueOf(amount)))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value(name))
            .andExpect(jsonPath("$.amount").value(amount));
    }
```

## TestRestTemplate
- RestTemplate은 REST API를 호출할 때 사용하는 Spring Framework에서 제공하는 클래스
- `spring-boot-starter-test`에 포함되어 있어 별도의 의존성 추가가 필요 없음
- `@WebMvcTest`는 JPA 기능이 작동하지 않음 JPA와 같이 사용 할 시 `@SpringBootTest`와 `TestRestTemplate`을 사용
- `TestRestTemplate`은 `@Autowired`로 주입 받음
```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class PostsApiControllerTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    public void Posts_등록된다() throws Exception {
        //given
        String title = "title";
        String content = "content";
        PostsSaveRequestDto requestDto = PostsSaveRequestDto.builder()
                .title(title)
                .content(content)
                .author("author")
                .build();

        String url = "http://localhost:" + port + "/api/v1/posts";

        //when
        ResponseEntity<Long> responseEntity = restTemplate.postForEntity(url, requestDto, Long.class);

        //then
        assertThat(responseEntity.getStatusCode()).isEqualTo(HttpStatus.OK);
        assertThat(responseEntity.getBody()).isGreaterThan(0L);

        List<Posts> all = postsRepository.findAll();
        assertThat(all.get(0).getTitle()).isEqualTo(title);
        assertThat(all.get(0).getContent()).isEqualTo(content);
    }
}
```

    
 
