# tacking Contexts와 z-index의 이해 (작성중)

### 🍒 개요 🍒
z-index는 많은 사람들이 알고 있지만 많은 사람들이 정확하게 모르는 속성중 하나입니다.<br>
제일 좋은 방법은 mdn 문서를 읽어보는 것이지만 모두 영어로 되어있어서 어려움이 있어,<br>
정리를 해야겠다는 생각에 정리를 하게되었습니다.<br><br>

제 생각에는 z-index를 정확하게 알고 사용하는 사람들이 적다고 생각합니다.<br>
그러니 저와 함께 문제를 풀면서, z-index의 정확한 개념을<br>
익혀보는 시간이 되었으면 좋겠습니다.

### ☠️ 문제 ☠️
<br><br>

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
<img width="202" alt="스크린샷 2023-01-06 오후 10 02 17" src="https://user-images.githubusercontent.com/89458455/211017538-669bea25-6c9b-4aaa-81ce-61219e1a41b9.png"><br>
링크 : [예시보기](https://summer-o3o.github.io/stacking-context/z-index_test1.html)<br>
빨간 ```<span>```을 아래 규칙을 깨지 않으면서 파랑과 초록 ```<span>``` 요소 밑으로 가게 해주세요.<br>
* HTML 마크업을 어떤 식으로든 건드려선 안 됩니다.<br>
* 어떤 요소에도 z-index를 추가하거나 변경해선 안 됩니다.<br>
* 어떤 요소의 position 속성도 추가하거나 변경해선 안 됩니다.<br>
( 정답은 스크롤을 내려보면 볼 수 있습니다. )<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>






##### [정답]<br>
빨간```<span>```의 부모인 ```<div>```에 opacity를 1보다 작게 주는 것이 정답입니다.<br><br>
<img width="207" alt="스크린샷 2023-01-06 오후 10 03 14" src="https://user-images.githubusercontent.com/89458455/211017660-820ccd3c-b1a6-4b26-b6c1-819eaffe3dea.png"><br><br>
링크 : [예시보기](https://summer-o3o.github.io/stacking-context/z-index_test1_1.html)<br>

```
div:first-child {
    opacity: .99;
}
```
