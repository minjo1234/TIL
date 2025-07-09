
| 특성      | `v-model`          | `:items`                    |
| ------- | ------------------ | --------------------------- |
| 데이터 바인딩 | 양방향 바인딩 (자동 업데이트)  | 단방향 바인딩 (수동 업데이트 필요)        |
|         |                    |                             |
| 사용 편리성  | 간편하게 선택된 값 관리      | 사용자 정의 로직에 맞게 수동으로 선택 관리    |
|         |                    |                             |
| 예시      | 고객 선택 및 ID 자동 업데이트 | 고객 목록 표시 및 버튼 클릭 시 선택된 값 처리 |

v-model :선택된 요소의 값이 자동으로 데이터모델에 반영된다. 사용자가 선택을하면 그 변화가 즉시 데이터 모델에 업데이트
(데이터를 다시 가공하여 바인딩하는 경우에 사용)

:items : 데이터를 UI에 표시하는 단방향 바인딩, 데이터만 표시하면 
데이터를 선택해도 자동으로 바인딩되지는 않는다.
(데이터를 다시 가공할필요없이 UI로 보여주는 경우에 사용)

---
#### items Example  

```html
<select :items="createVue.customers" multiple="multiple" style="width: 100%;">
<option v-for="customer in customers">
	{{customer.name}}
</option>					
<p>선택된 값 : 없음 </p>
</select>
```

#### v-model Example

```html
<select v-model="selectedCustomer" multiple="multiple" style="width: 100%;">
<option v-for="customer in customers" :key="customer.Id" :value="customer.name">
	 {{customer.name}}
 </option>		
<p>선택된 값 : {selectedCustomer} </p> 
</select>
```

:key -> key값과
:value -> value값을 설정하여 데이터를 다시 가공할 수 있다.
