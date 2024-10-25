

$_ajax 


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