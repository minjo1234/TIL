
### box model의 전체 크기

: 콘텐츠 크기 + padding 값 + boarder 값 + margin 값


```css

div{
  background: pink;
  padding: 50px;
  margin: 50px;
  border: 50px solid rgb(162, 90, 162);
  width: 300px;
}
```

- width값이 300px인 div 박스를 하나 만들어보고 해당 박스의 크기를 확인해보면 다음과 같다.
- 300 + 100 (padding 값) + 100 (boarder값) + 100(margin값) = 600


개발자는 300px의 box를 만들려고 하였지만<font color="#ff0000"> 480px 사이즈의 box가</font> 만들어지는 것을 확인할 수 있다.
내가 지정한 width나 height을 통해서 box를 만들려고 하는 경우에 사용하는 속성이 **border-box** 속성이다.

초기값은 content-box로 설정되어 있고 box-sizing을 지정해주지 않으면 content-box 형식으로 요소의 너비와 높이를 계산한다.

- content-box :  
- border-box :   


