
th:fragment : 반복되는 코드를 재사용 

th:replace -> th:fragment () 블럭이나 외부 템플릿으로 값을 전달하고 해당 템플릿을 사용하는 경우 
th:replace -> 블럭이나 외부 템플릿을 단순히 가져와서 사용하는 경우 

```javascript
<th:block th:replace="~{techsupport/popup/tab/ticketInfo}"></th>
```


```javascript

<th:block th:replace="~{techsupport/popup/tab/ticketInfo:: modal('id' , 'request' )}"></th>

<th:block th:fragment="modal(id, type)">
</th>
```
