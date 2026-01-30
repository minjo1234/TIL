

$_ajax 일반

1.콜백 방식


Ajax는 비동기로 동작하고 있기 때문에, 함수가 종료되기 전에 Ajax 요청이 완료되지 않는다.

```javascript 

checkAlreadyIsExistsSalesTarget() {
    let tmpDepartmentId = this.salesTargetCondition.departmentId;
    this.salesTargetCondition.departmentId = this.currentUser.departmentId;

    $.ajax({
        type: 'post',
        url: `${contextPath}/api/salesTarget/find/searchCondition`,
        dataType: 'json',
        async: false, // 이 값을 true로 하면 비동기로 동작
        data: JSON.stringify(copyObject(this.salesTargetCondition)),
        contentType: 'application/json; charset=utf-8',
        success: (dtos) => {
            this.salesTargetCondition.departmentId = tmpDepartmentId;

            if (dtos.find(dto => dto.employeeId == this.currentUser.userId)) {
                return true;  // 콜백 안에서만 반환되고, 외부로는 전달되지 않음
            } else {
                return false;
            }
        }
    });

    // 여기서 함수가 끝나기 때문에 success 콜백 내의 return 값이 전달되지 않음
}


```

### 2. Promise ()

- 비동기 방식이지만 비동ㅣ 작업의 완료또는 실패 시점에 값을 처리할 수 있다.

return new Promise((resolve, reject => {
	
})) 

```javascript
checkAlreadyIsExistsSalesTarget() {
    let tmpDepartmentId = this.salesTargetCondition.departmentId;
    this.salesTargetCondition.departmentId = this.currentUser.departmentId;

    // 비동기 작업을 Promise로 처리
    return new Promise((resolve, reject) => {
        $.ajax({
            type: 'post',
            url: `${contextPath}/api/salesTarget/find/searchCondition`,
            dataType: 'json',
            data: JSON.stringify(copyObject(this.salesTargetCondition)),
            contentType: 'application/json; charset=utf-8',
            success: (dtos) => {
                this.salesTargetCondition.departmentId = tmpDepartmentId;

                if (dtos.find(dto => dto.employeeId == this.currentUser.userId)) {
                    resolve(true);  // Promise가 완료되었을 때 값을 반환
                } else {
                    resolve(false);  // Promise가 완료되었을 때 다른 값을 반환
                }
            },
            error: (error) => {
                reject(error);  // 에러 발생 시
            }
        });
    });
}
```


## 3.Promise 사용방식


```java
checkAlreadyIsExistsSalesTarget().then(isExists => {
    if (isExists) {
        console.log("이미 판매 목표가 존재합니다.");
    } else {
        console.log("판매 목표가 존재하지 않습니다.");
    }
}).catch(error => {
    console.error("에러 발생:", error);
});

```

.then을 이용하거나 async/await를 사용해서 비동기 작업이 끝나기 전에는 값을 받을 수 없다.

