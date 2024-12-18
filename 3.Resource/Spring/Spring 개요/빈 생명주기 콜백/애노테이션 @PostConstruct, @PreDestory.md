

InitializingBean, DisposableBean 대신에
`@PostConstruct` , `@PreDestory` 어노테이션을 사용할 수 있습니다.

#### @PostConstruct, @PreDestory 애노테이션 특징

- 최신 스프링에서 가장 권장하는 방법이다.
- 애노테이션 하나만 붙이면 된다.
- javax.annotation.PostConstruct 스프링에 종속적인게 아니라 자바 표준 기술이다.
- 컴포넌트 스캔과 잘 어울린다.
- 유일한 단점은 외부 라이브러리에는 적용하지 못한다는 점이다.
- 외부 라이브러리 초기화, 종료 해야하면 @Bean의 기능을 사용하자.

---

### 정리

- @PostConstruct, @PreDestroy 어노테이션을 사용하자.
- 코드를 코칠 수 없는 외부 라이브러리의 경우에는 Bean, initMethod, destroymethod를 활용하자.


function clearObject(obj) {  
    Object.keys(obj).forEach(key => {  
        obj[key] = '';  
    })  
}  
  
function copyObject(obj) {  
    return JSON.parse(JSON.stringify(obj));  
}  
  
function _ajax(type, url, data, callback) {  
    $.ajax({  
        type: type,  
        url: url,  
        dataType: 'json',  
        async: false,  
        data: data,  
        contentType: 'application/json; charset=utf-8',  
        success: (data) => {  
            if (callback) callback(data);  
        },  
        error: (xhr) => {  
            let json = JSON.parse(xhr.responseText);  
            (json != '' || json != null || json != undefined) ? alert(json.customMessage) : alert(xhr);  
        }  
    })  
}  
  
  
function initSelect2(selector, parentSelector, data, key, title, setValue = '') {  
    $(selector).empty().select2('destroy');  
    $(selector).select2({  
        dropdownParent: $(parentSelector),  
        theme: 'bootstrap4',  
        data: data.map(d => {  
            return {id: d[key], text: d[title]}  
        })  
    });  
    $(selector).val(setValue).trigger('change');  
}