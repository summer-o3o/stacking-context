# tacking Contexts와 z-index의 이해 (작성중)

### 🍒 개요 🍒
z-index 는 많은 사람들이 알고 있지만 많은 사람들이 정확하게 모르는 속성중 하나입니다.<br>
제일 좋은 방법은 mdn 문서를 읽어보는 것이지만 모두 영어로 되어있어서 어려움이 있습니다~ <br>
이제 z-index 와 Stacking Contexts 라는 것에 대해 저와 함께 알아봅시다.<br><br>

게다가 z-index는 실제로 정확하게 알고 있는 사람들이 적다고 생각합니다.<br>
( 실제로도 적긴하다 😵‍💫 )<br>

### ☠️ 문제 ☠️
다음 문제를 풀어보자.<br><br>

```
<div>
  <span class="red">Red</span>
</div>
<div>
  <span class="green">Green</span>
</div>
<div>
  <span class="blue">Blue</span>
</div>
.red, .green, .blue {
  position: absolute;
}
.red {
  background: red;
  z-index: 1;
}
.green {
  background: green;
}
.blue {
  background: blue;
}
```

##### [문제 1]<br>
[예시보기](https://summer-o3o.github.io/stacking-context/z-index_test1.html){: target="_blank"}<br>
빨간 ```<span>```을 아래 규칙을 깨지 않으면서 파랑과 초록 ```<span>``` 요소 밑으로 가게 하시오.<br>
* HTML 마크업을 어떤 식으로든 건드려선 안 된다.<br>
* 어떤 요소에도 z-index를 추가하거나 변경해선 안 된다.<br>
* 어떤 요소의 position 속성도 추가하거나 변경해선 안 된다.<br>
( 해답은 스크롤을 내려보면 볼 수 있다. )<br><br><br><br><br><br><br><br><br><br>





##### [정답]<br>
빨간```<span>```의 부모인 ```<div>```에 opacity를 1보다 작게 주는 것이다.<br>
[예시보기](https://summer-o3o.github.io/stacking-context/z-index_test1_1.html){: target="_blank"}<br>

```
div:first-child {
    opacity: .99;
}
```
