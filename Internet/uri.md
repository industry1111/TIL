## URI(Uniform Resource Identifier)
인터넷에서 리소스를 고유하게 식별하는 데 사용되는 문자열입니다. URI는 웹 상의 모든 리소스를 식별하고 참조할 수 있는 통합된 방법을 제공한다.
- **U**niform : 리소스를 식별하는 통일된 방식
- **R**esource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- **I**dentifier : 다른 항목과 구분하는데 필요한 정보


URI는 **URL**과 **URI**로 구분할 수 있다.

**URL (Uniform Resource Locator)**
리소스의 `위치(Locater)`를 나타내며, 특정한 인터넷 주소를 사용하여 리소스에 `직접 접근`할 수 있도록 한다.

**URN (Uniform Resource Name)**
리소스의 `이름(Name)`을 나타내며, 리소스의 위치와 상관없이 고유한 식별자를 제공해 URN을 통해 리소스가 어디에 위치해 있는지와는 관계없이 고유한 식별자로 `리소스를 참조`할 수 있다. 하지만 실제 리소스에 직접 접근하기 위해선 추가적인 별도의 매커니즘이 필요하다.
URN 이름만으로 실제 리소르를 찾을 수 있는 방법이 보편화 되지 않음

<img width="90%" src ="https://velog.velcdn.com/images/industry1111/post/3516d580-b5d7-408a-ac31-eeba6c6bac43/image.png">

### URL
구조
- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello&hl=ko

`scheme`
- **https:**//www.google.com:443/search?q=hello&hl=ko
- 주로 프로토콜 사용
  예) http, https, ftp 등등

- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

`userinfo`
- scheme://**[userinfo@]**host[:port][/path][?query][#fragment]
- URL에 사용자정보를 포함해서 인증 거의 사용하지 않음

`host`
- scheme://[userinfo@]**host**[:port][/path][?query][#fragment]
- https:// **www.google.com**:443/search?q=hello&hl=ko
- 호스트명
- 도메인명 또는 IP 주소를 직접 사용가능

`path`
- scheme://[userinfo@]host[:port]**[/path]**[?query][#fragment]
- https://www.google.com:443/ **search**?q=hello&hl=ko
- 리소스 경로(path), 계층적 구조 예)
- /home/file1.jpg
- /members

`query`
- scheme://[userinfo@]host[:port][/path]**[?query]**[#fragment]
- https://www.google.com:443/search **?q=hello&hl=ko**
- key=value 형태
- ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

`fragment`
- scheme://[userinfo@]host[:port][/path][?query]**[#fragment]**
- https://velog.io/@industry1111/URI와-웹-브라우저#uriuniform-resource-identifier
- fragment
- html 내부 북마크 등에 사용 (velog나 깃허브의 목차라고 생각)
- 서버에 전송하는 정보 아님