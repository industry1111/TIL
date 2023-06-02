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


    
 
