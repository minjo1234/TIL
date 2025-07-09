
Multipart/form-data

HTML에서는 파일 업로드를 위한 폼 전송방식에는 두 가지가 존재한다.

1.application/x-www-form-urlencoded
2.multipart/form-data

1번 방법은 파일을 전송할 때 url만 보내는 경우가 거의없어 (이름, 나이, 프로필 사진)

1.파일의 바이너리코드(이진코드)들을 이용해서 url을 넘기는데 url이 길어지며 
2.일반 문자와 바이너리 코드들을 동시에 전송해야 하는 문제가 발생한다.

==**3.그래서 대부분 multipart/form-data 방식을 지향하고 있다.**==

```html
<form th:action method="post" enctype="multipart/form-data></form>
```


### Servlet 방식

HttpServletRequest 넘긴다면 파라미터와 파일들을 모두 받을 수 있다.

1.spring 옵션 중에 spring.servlet.multipart.enabled라는 옵션이 존재하는데 옵션을 켜주면 
2.enctype="multipart/form-data 로 넘어오는 경우는 서블릿 컨테이너가 
**3.HttpServletRequest를 MultipartHttpServletRequest로 변환해서 반환해준다.**

MultipartHttpServletRequest는 HttpServlet의 자식 인터페이스로 관련된 추가 기능이 존재한다.

---

@RequestParam MultiFile file vs MultipartFile fileRequest

---

```java
@PostMapping("/upload)
public String handleFileUpload(@RequestParam MultiFile file) { 
	// file process logic
}
```


```java
@PostMapping("/upload)
 public String handleFileUpload(MultipartHttpServletRequest request){
	 MultipartFile file = request.getFile("file);
 }
```









