# 파일 업로드

### HTML 파일 전송 방식
html 파일 전송 방식을 이해하기 위해선 아래와 같은 2가지 방식의 폼 전송방식을 이해
- application/x-www-form-urlencoded
- multipart/form-data

#### application/x-www-form-urlencoded
- html에서 form 데이터를 서버로 전송하는 기본적인 방법
```html
<form method="post">
    아이디 <input type="text" name="id">
    이름 <input type="text" name="name">
    비밀번호 <input type="text" name="password">
    <button type="submit">전송</button>
</form>
```
해당 웹브라우저가 생성한 요청 HTTP 메시지
```http request
POST /save HTTP/1.1
Host: localhost:8080
Content-Type: application/x-www-form-urlencoded //Form 태그에 별도의 enctype 옵션이 없으면 해당 내용 추가

id=industry1111&name=gudrb&password=1234
```
파일은 문자가 아니라 바이너리 데이터를 전송해야하므로 이 방식으로는 전송하기는 어렵다.
`문자와 바이너리르 동시에 전송`

#### multipart/form-data
```html
<form method="post" enctype="multipart/form-data">
    아이디 <input type="text" name="id">
    이름 <input type="text" name="name">
    비밀번호 <input type="text" name="password">
    첨부파일 <input type="file" name="file1">
    <button type="submit">전송</button>
</form>
```

```http request
POST /save HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data; boundary=----XXX

------XXX
Content-Disposition: form-data; name="id"

industry1111
------XXX
Content-Disposition: form-data; name="name"

gudrb
------XXX
Content-Disposition: form-data; name="password"

1234
------XXX
Content-Disposition: form-data; name="file1" filename="image.png"
Content-Type: image/png

1111231asa0ada01jad01add48aad...
------XXX--
```
- `multipart/form-data` 방식은 다른 종유릐 여러 파일과 폼의 내용을 함께 전송할 수 있다.
- 각각의 항목(part)을 구분해서, 한번에 전송

### multipart 사용 옵션

```properties
#multipartFile 사용여부
spring.servlet.multipart.enabled=true
#파일하나 최대 크기
spring.servlet.multipart.max-file-size=10MB
#multipart 요청의 전체 데이터 크기
spring.servlet.multipart.max-request-size=10MB

#Http 요청 메시지 로깅
logging.level.org.apache.coyote.http11=debug;

#스토리지 경로 설정
file.storage.path = /Users/gohyeong-gyu/Downloads/upload/
```

application.properties에 설정한 `file.storage.path`는 `@Value`로 주입 할 수있다.

```java
@Value("${file.storage.path}")
private String storagePath;
```

### Spring MultipartFIle 사용

```java
pulbic class SpringUploadController {
    
    @PostMapping("/upload")
    public String saveFile(@RequestParam String itemName, @RequestParam MultipartFile multipartFile, HttpServletRequest request) {
        log.info("request={}", request);
        log,info("itemName={}", itemName);
        log.info("multipartFile={}", multipartFile);
        
        Strin fullPath = storagePath + multipartFile.getOriginalFilename();
        multipartFile.transferTo(new File(fullPath));
        
        return "view";
    }
    
}
```
- 파일 저장시 중복충동을 피하기위해 UUID를 사용하거나 FileName +'_' + 업로드시간 을 이용하영 저장
```java
package com.travel.web_oasis.domain.service;

import com.travel.web_oasis.domain.files.FileAttach;
import com.travel.web_oasis.domain.repository.FileAttachRepository;
import groovy.util.logging.Slf4j;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;
import org.springframework.web.multipart.MultipartFile;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.UUID;
import java.util.stream.Stream;

@Slf4j
@Service
public class FileAttachServiceImpl implements FileAttachService {

    @Autowired
    private FileAttachRepository fileAttachRepository;

    @Value("${file.storage.path}")
    private  String storagePath;
    private static final Logger logger = LoggerFactory.getLogger(FileAttachServiceImpl.class);

    @Override
    public List<FileAttach> upload(List<MultipartFile> multipartFiles) {
        List<FileAttach> fileAttachments = new ArrayList<>();

        for (MultipartFile multipartFile : multipartFiles) {
            FileAttach fileAttach = uploadSingleFile(multipartFile);
            fileAttachments.add(fileAttach);
        }

        return fileAttachments;
    }

    private FileAttach uploadSingleFile(MultipartFile multipartFile) {
        String fileUrl = "http://localhost:8080/files/"; // 파일 URL 설정 -> 환경변수로 설정 예정
        String fileName = multipartFile.getOriginalFilename();
        String fileContentType = multipartFile.getContentType();

        String fileStorageName = saveFileToStorage(multipartFile);
        logger.info("fileName : {} , fileContentType : {}", fileName, fileContentType);
        return FileAttach.builder()
                .fileName(fileName)
                .fileStoreName(fileStorageName)
                .fileUrl(fileUrl + fileName)
                .FileType(fileContentType)
                .fileSize(multipartFile.getSize())
                .build();
    }


    /* 업로드한 파일을 저장소에 저장
    * Param
    *  multipartFile : 사용자가 화면상에서 업로드한 파일
    *
    * return : 저장시 UUID로 생성된 파일명
    * */
    private String saveFileToStorage(MultipartFile multipartFile) {

        String originalFilename = multipartFile.getOriginalFilename();

        String storeFileName = createStoreFilename(originalFilename);

        try {
            //저장경로 + 파일이름의 위치에 파일생성
            multipartFile.transferTo(new File(getFullPath(storeFileName)));
        } catch (Exception e) {
            e.printStackTrace();
        }
        return storeFileName;
    }

    /* UUID를 이용한 파일명 생성
    * Param
    *  originalFileName : 사용자가 실제 업로드한 파일명 (logo.png)
    *
    * return : UUID + '.' + 확장자*/
    private String createStoreFilename(String originalFilename) {

        //확장자
        String ext = extracted(originalFilename);

        String uuid = UUID.randomUUID().toString();

        return uuid + "." + ext;
    }

    /* 파일 확장자 추출
    * Param
    *  originalFileName : 사용자가 실제 업로드한 파일명 (logo.png)
    *
    * return : 파일 확장자 (png)
    * */
    private String extracted(String originalFileName) {
        int pos = originalFileName.lastIndexOf('.');
        return originalFileName.substring(pos + 1);
    }

    /*저장 경로
    * Param
    *  fileName : UUID.확장자가 붙은 파일명
    *
    * return : 저장경로
    * */
    @Override
    public String getFullPath(String fileName) {
        return storagePath + fileName;
    }
    
    @Override
    public String getFileType(String fileName) {

        return fileAttachRepository.findByFileStoreName(fileName).getFileType();
    }
}


```

### 화면상에서 업로드한 파일 가져오기

#### 서버

```java
@ResponseBody
    @GetMapping("/download/{fileName}")
    public ResponseEntity<Resource> downloadImage(@PathVariable String fileName) throws MalformedURLException {
        Resource resource = new UrlResource("file:" + fileAttachService.getFullPath(fileName));

        if (resource.exists()) {
            String contentType = fileAttachService.getFileType(fileName);
            return ResponseEntity.ok()
                    .contentType(MediaType.parseMediaType(contentType))
                    .body(resource);
        } else {
            return ResponseEntity.notFound().build();
        }
    }
```

#### 화면
- 비동기 방식으로 요청및 응답하기위해 작성한 ajax함수이며 요청값에 따라 보내는 방식이 다르다.
- 파일을 업로드하는 경우
  - 자바스크립트에서 파일을 업로드할 경우 `FormData`를 사용하기 대문에 매개변수 data의 인스턴스를 확인
- 파일을 가져오는 경우 
  - `responseType: 'blob'` 으로 주지않으면 status : 200 으로 성공이나 `statustext : parsererror` 가 발생해 error핸들러로 응답된다.
```javascript

/*
* method: 요청 방식(GET, POST, PUT, DELETE)
* url: 요청 url (/post/{id}/{fileName})
* GET 요청일 경우 데이터는 아래 형식으로
* data: {
    pahParams: {
        id: 1
        fileName : file
    }
    queryParams : {

    }
 }
* submitFunc: 성공시 콜백 함수
* errorFunc: 실패시 콜백 함수 ==> 공통함수로 처리 예정
* */
function customAjax(method, url, data, submitFunc, errorFunc) {
    const ajaxOptions = {
        url: url,
        method: method,
        success: function(result, status, xhr) {
            if (submitFunc != null) {
                submitFunc(result, xhr);
            }
        },
        error: function(request, status, error) {
            if (errorFunc != null) {
                errorFunc(request, status, error);
            } else {
                console.log("에러");
            }
        },
        complete: function() {
            console.log("무조건 실행");
        }
    };

    if (method === "GET") {
        if (data.pathParams) {
            // 경로 변수를 사용하는 경우
            url = url.replace(/{(\w+)}/g, function(match, pathParam) {
                return data.pathParams[pathParam];
            });
        }
        ajaxOptions.data = data.queryParams;
    } else {
        // 파일 업로드인 경우
        if (data instanceof FormData) {
            ajaxOptions.data = data;
            ajaxOptions.processData = false;
            ajaxOptions.contentType = false;
        } else {
            ajaxOptions.data = JSON.stringify(data);
            ajaxOptions.contentType = "application/json";
        }
    }

    ajaxOptions.url = url;

    if (url.includes("download")) {
        ajaxOptions.xhrFields = {
            responseType: 'blob' // 파일을 받아오기 위해 responseType을 'blob'으로 설정
        }
    }

    $.ajax(ajaxOptions);
}
```


