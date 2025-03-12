
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


-- 는 하나만 사용하는 것을 권장하며


-------
