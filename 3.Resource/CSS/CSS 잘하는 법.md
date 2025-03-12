
### 1.selector를 잘 사용하자.

> 과거에는 html을 최대한 건들지 않고 css만으로 디자인을 하는것이 중요했다.
> 하지만 지금은 웹 프레임워크 위에서 html과 css를 묶어 컴포넌트로 다루는 방식으로 진화했다.
> 그래서 selector가 복잡할수록 오히려 html을 수정하는데 문제가 더 발생한다.


BEM만 잘 이해해도 좋다.

```html
<div class="header">
  <div class="nav"></div>
</div>

<style>
.header .nav { (X) } /* 이렇게 하면 nav가 header 구조에 종속이 된다. */
</style>
```


```html
<div class="header">
  <div class="header__nav"></div>
</div>

<style>
.header__nav { (O) } /* 구조도 표현하면서 종속 관계가 없다. */
</style>
```


> [!NOTE]
> -- 는 하나만 사용하는 것을 권장하며 2depth로 작성된다면 컴포넌트를 분리해야 한다는 신호이다.

-------


> [!CSS는 레이아웃인 것과 레이아웃이 아닌것으로 구성된다.] 
> 
> #### 레이아웃이 아닌것
> - 글자
> - 색상, 배경
> - 테두리
> - 그림자
> - 투명도
> - 필터

- 대부분 간단하다.
----


> [!CSS] 
> #### 레이아웃 
> - 대부분 flexbox로 가능하다. (과도기가 있었지만)
> - margin을 적당히 사용하자. (framework에 margin이 있다면 컴포넌트 배치가 어려울 수 있다.)
> - overlay 공부 ( z축 관련)


`row` | `column` 보다는 `horizontal` | `vertical`로  
`align-items` | `justify-content` 보다는 `top+right`로
hbox와 달리 vbox는 `align-items: stretch`으로 만드는 것이 좋기 때문에 저는 아래와 같이 만들어서 사용하고 있습니다.

### vbox는 숙제입니다.

어렵지 않으실 거예요. vbox는 hbox와 방향만 다를 뿐 동일합니다.  
hbox와 달리 vbox는 `align-items: stretch`으로 만드는 것이 좋기 때문에 저는 아래와 같이 만들어서 사용하고 있습니다.


------



 css 잘하는법 


https://velog.io/@teo/CSS-%EA%B3%B5%EB%B6%80-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%B4%EC%95%BC-%ED%95%98%EB%82%98%EC%9A%94-%EC%9D%B4%EB%A1%A0%ED%8E%B8-feat.-figma


