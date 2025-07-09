
	
1.th:inline 서버 사이드 변수의 값을 클라이언트 사이드로 전달할 때 유용 - ${}

```javascript
th:inline="javascript"
```


```javascript
1.<th:block th:replace="/경로"></th:block>
2.<th:block th:fragment="modal(id,type)"></th:block>

```


현재 위치에 다른 템플릿의 조각을 삽입(replace) 하는 문법입니다.


3.thymeleaf 매개변수 전달하는 경우에 두 가지로 분류되어 문법이 사용된다.

```javascript
<button type="button" class="btn btn-primary" th:id="|${id}_modalButton|" th:onclick="purchasePopup([[${id}]])"></button>
```

| ... | : 문자열과 변수를 결합할 때 사용한다.
${} : 단독으로 변수를 출력할 때 사용된다.
[${}] : 자바스크립트 내부에서 동적으로 사용하지만 배열이 아닌경우
[[${}]]  : [[]] 자바스크립트내부에서 동적으로 사용하지만 배열인 경우를 지칭
```html
<p th:text=${message}>Default Text</p>
```

```html
<script>
	var message = [[${messages}]];
	var message = [${messages}] 
</script>
```

  
\