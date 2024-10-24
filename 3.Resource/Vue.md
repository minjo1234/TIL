
### `find`

- **목적**: 배열에서 조건에 맞는 첫 번째 요소를 찾습니다. 조건을 만족하는 요소가 있을 경우, 해당 요소를 반환하며, 조건을 만족하는 요소가 없으면 `undefined`를 반환합니다.
- **사용 예**: 특정 조건을 충족하는 첫 번째 객체를 찾을 때 사용됩니다.
- **구문**:
    
    javascript
    
    코드 복사
    
    `const foundElement = array.find(element => {     return element.condition; // 조건을 만족하는 첫 번째 요소를 찾습니다. });`
    

### `filter`

- **목적**: 배열에서 조건에 맞는 모든 요소를 추출하여 새로운 배열을 만듭니다. 조건을 만족하는 요소가 없으면 빈 배열을 반환합니다.
- **사용 예**: 특정 조건을 충족하는 모든 요소를 모으고 싶을 때 사용됩니다.
- **구문**:
    
    javascript
    
    코드 복사
    
    `const filteredArray = array.filter(element => {     return element.condition; // 조건을 만족하는 모든 요소를 포함합니다. });`
- 