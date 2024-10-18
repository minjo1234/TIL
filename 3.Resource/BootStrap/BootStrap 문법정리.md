
```html
<div class="mb-1 row" data-row-type="boot" required="required"> 
<label class="col-sm-2 col-form-label fs-6">작업 티켓명</label>
<div class="col-sm-9>
			<input v-model="purchase.title" type="text" class="form-control fs-13-px placeholder="작업 티켓명을 기입해주세요." maxlength="80">
			</div>
</div>
```


row : grid 시스템에서 행(row) 를 결정한다.
.col-form-label : row를 사용할때는 .col-*-*을 지정하여 라벨이나 컨트롤의 폭을 지정, <label>에는 반드시, .col-form-label을 추가하여 
폼 컨트롤과 함께 수직 방향의 중앙에 배치 , 해당 태그가 존재하지 않을경우 그리드 시스템의 적용을 받지않아 인라인 요소로 배치된다.
fs-13-px : 폰트크기를  13px로 지정한다.

col-form-control : 입력 필드(input), 선택 목록(select), 텍스트 영역(textarea)와 같은 다양한 폼 요소에 일관 된 스타일을 적용시켜준다.
col-sm-1 ~  : 그리드 클래스에서 열의 크기를 지정한다

매우 작은 기기(모바일) : 너비가 768px 미만인 화면 .col-xs-*
작은 기기(태블릿) - 너비가 768px 이상인 화면 col-sm 
중간 기기(노트북) - 너비가 992px 이상인 화면 col-md-*
큰 기기(노트북/데스크탑) - 너비가 1200px 이상인 화면 .col-lg-*

form-control : bootstrap의 기본적인 style 요소들이 자동으로 적용됩니다.

- **높이와 너비**: 폼 요소가 가로로 100% 너비를 차지하게 되어 부모 요소의 너비에 맞게 확장됩니다.
- **테두리**: 기본적으로 부드러운 둥근 모서리(border-radius)가 적용되고, 테두리 색상은 입력 필드의 상태에 따라 다릅니다.
- **패딩**: 입력 필드 내부에 적절한 패딩이 설정되어 텍스트가 입력되었을 때 여백이 적절히 유지됩니다.
- **폰트**: 입력 필드에 들어가는 텍스트에 대한 기본적인 폰트 크기와 스타일이 설정됩니다.
- **포커스 상태**: 사용자가 필드를 클릭하면 파란색 포커스 스타일이 자동으로 적용됩니다.

fs- 속성들은 폰트를 의미한다.


---------


.attr vs .css 

.attr - 해당 내역의 속성을 가져오는 경우
.css - style 관련된 속성을 가져오는 경우


purchaseInfo -> purchaseInfoTest 이동후 이름변경 예정

flex:4 flex:5 비율이 4와 5만큼의 비율이 차지하도록 지정한다.


---


### fs (font-size)


- **`fs-1`**: 2.5rem (40px)
- **`fs-2`**: 2rem (32px)
- **`fs-3`**: 1.75rem (28px)
- **`fs-4`**: 1.5rem (24px)
- **`fs-5`**: 1.25rem (20px)
- **`fs-6`**: 1rem (16px)

waitCreateElement('.adoptedCustomer-dropdown-item', this.customers, () => {  
    $(".adoptedCustomer-dropdown-item[value=" + dto.adoptedCustomer.id + "]").click();

복합키관련

computed - vue 에서 변화를 반영하여 자동으로 업데이트 되는 속성
data가 변하게 될 경우 computed안에 있는 Method도 업데이트가 되어 