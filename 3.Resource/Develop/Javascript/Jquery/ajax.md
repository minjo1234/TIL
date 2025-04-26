
#### 1.multipart/form-data

```javascript
_save2() {  
    if (this.validate()) {  
        $.ajax({  
            url: `${contextPath}/api/business/director/save`,  
            type: "POST",  
            enctype: "multipart/form-data",  
            async: false,  
            data: this.getDTO(),  
            processData: false,  
            contentType: false,  
            error: function (jqXHR, textStatus, errorThrown) {  
                alert('업로드 중 문제가 발생하였습니다! 지속될 시 관리자에게 문의해주세요.');  
                successFlag = false;  
                console.log(jqXHR);  
                console.log(textStatus);  
                console.log(errorThrown);  
            }  
        })  
    }  
}
```

processData : ajax로 전송할때 processData(자동으로 데이터를 변환)를 자동으로 설정해주는데 파일형태이기 때문에 false로 설정한다.

contentType : ajax로 전송할때 contentType(브라우저가 적절한)을 자동으로 설정해주는데 파일형태이기 때문에 false로 설정한다.