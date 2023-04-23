# tacking Contexts와 z-index의 이해

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
<img width="202" alt="스크린샷 2023-01-06 오후 10 02 17" src="https://user-images.githubusercontent.com/89458455/211017538-669bea25-6c9b-4aaa-81ce-61219e1a41b9.png"><br>
링크 : [예시보기](https://summer-o3o.github.io/stacking-context/z-index_test1.html)<br>
빨간 ```<span>```을 아래 규칙을 깨지 않으면서 파랑과 초록 ```<span>``` 요소 밑으로 가게 하시오.<br>
* HTML 마크업을 어떤 식으로든 건드려선 안 된다.<br>
* 어떤 요소에도 z-index를 추가하거나 변경해선 안 된다.<br>
* 어떤 요소의 position 속성도 추가하거나 변경해선 안 된다.<br>
( 해답은 스크롤을 내려보면 볼 수 있다. )<br><br><br><br><br><br><br><br><br><br>






##### [정답]<br>
빨간```<span>```의 부모인 ```<div>```에 opacity를 1보다 작게 주는 것이다.<br><br>
<img width="207" alt="스크린샷 2023-01-06 오후 10 03 14" src="https://user-images.githubusercontent.com/89458455/211017660-820ccd3c-b1a6-4b26-b6c1-819eaffe3dea.png"><br><br>
링크 : [예시보기](https://summer-o3o.github.io/stacking-context/z-index_test1_1.html)<br>

```
div:first-child {
    opacity: .99;
}
```

<br><br><br>

### 🍒 쌓임 맥락(Stacking Contexts) 🍒
먼저 쌓임 맥락을 설명하는게 순서에 안맞는거 같긴 하지만 먼저 설명해야 아래 내용도 이해가 쉽기 때문에 적는다.<br><br>

쌓임 맥락이란 **같은 부모 밑에 있어서 쌓임 순서에 따라 함께 앞 뒤로 한꺼번에 움직일 수 있는 요소들의 그룹**이다.<br>
쌓임 맥락은 다음 셋 중 하나에 속할 때 만들어진다. (3+1)<br>

- 문서의 뿌리 요소인 <html> 요소
- 요소의 position 값이 static이 아니면서 z-index도 auto가 아닐 때 (z-index:auto는 디폴트 값으로 z-index를 사용 안한것과 같다.)
- opacity 값이 1보다 작을 때
- [ 모바일 웹킷과 크롬 22 이상에서, position:fixed는 z-index가 auto 여도 무조건 새로운 쌓임 맥락을 만든다. ]<br><br>

다음 예제 파일에서 **Division Element #3** 를 보면 모든 자식 요소들은 부모의 쌓임 맥락 안에서만 유효하다는 것을 알 수 있다.<br>
같은 선상에 있는 DIV 1, DIV 2, DIV 3 들의 쌓임 순서가 z-index값에 의해서 5, 2, 4 이지만 DIV 4는 z-index가 6인데도 불구하고<br>
**z-index 값이 5인 DIV 1 밑에 렌더링 된다.**<br>
이것으로 DIV 3의 자식요소들은 쌓임 순서가 부모의 쌓임 맥락안에 있다는 것을 알 수 있다.

링크 : [예시보기](https://summer-o3o.github.io/stacking-context/stacking_contexts.html)<br>
<img width="400" alt="Untitled" src="https://user-images.githubusercontent.com/89458455/233829852-c863f67f-a5dc-4f92-97ec-92d986bfc6ad.png">

- 뿌리 엘리먼트
    - DIV #1
    - DIV #2
    - DIV #3
        - DIV #4
        - DIV #5
        - DIV #6

<br><br><br>

### 🍒 쌓임 순서(Stacking Order) 🍒
z-index는 간단해보인다. 값이 높은것이 값이 낮은거 위에 렌더링 된다.<br>
**하지만 실제로는 이게 다가 아니고 생각만큼 단순하지 않다.**<br><br>

HTML 문서의 모든 요소는 다른 요소의 앞이나 뒤로 들어갈 수 있는데 이걸 쌓임 순서(stacking order)라고 한다.<br>
이 순서를 정하는 규칙은 스펙에 상당히 명확하게 정의돼 있다.<br>
**하지만 많은 개발자들이 이것들을 완전히 이해하고 있지 못한다.**<br><br><br>

- z-index와 position 속성이 없을 때는 기본적으로 HTML에 작성된 순서와 같다.
    
    (실제론 조금 복잡하다. [https://www.w3.org/TR/CSS2/zindex.html](https://www.w3.org/TR/CSS2/zindex.html) )
    
- 아래 그림과 같이 position 속성을 요소에 사용할 때, static이 아닌 position속성이 있는 모든 것들은 position 속성이 없는 일반적인 요소들 앞에 렌더링된다.
<br>(사용자 눈과 더 가까운)<br>
위에 쌓임 맥락에서 설명한것처럼 opacity 값이 1보다 작은 요소도 이와 같은 레벨의 쌓임 순서를 가지게 된다.<br>
그리고 이것들은 html 작성 순서에 따라 쌓임 순서가 정해진다.<br>
링크 : [예시보기](https://summer-o3o.github.io/stacking-context/stacking_order.html)<br>
<img width="400" alt="Untitled" src="https://user-images.githubusercontent.com/89458455/233830100-c0b6380d-db96-44b4-9d09-9b9dd125233c.png">
<br><br>

링크 : [예시보기](https://summer-o3o.github.io/stacking-context/stacking_order2.html)<br>
<img width="400" alt="Untitled2" src="https://user-images.githubusercontent.com/89458455/233830136-2170e4a9-4aa7-4f8d-909a-eb95d990762f.png"><br><br>

- z-index가 연관되면 좀 더 복잡해진다.
- **당연히 알고 있겠지만 position 속성을 쓰지 않으면 z-index 값은 작동하지 않는다.**
**여기서 static이 아닌 position 속성이 부여되었을 때의 z-index값은 쌓임 맥락(stacking contexts)를 만들어낸다.**
- 쌓임 맥락에 대한 설명을 상기시켜보면, 자식요소에 z-index 값을 아무리 낮추거나 높여도 부모중에 (ex. position:relative;z-index:-10 을 가진 부모) 쌓임 맥락이 있다면 그 쌓임 맥락 밑이나 그 위로 뚫고 나갈 수가 없다.
반대로 말하면 부모중에 쌓임 맥락이 없는 곳까지 z-index 값에 따라 한도 끝도 없이 밑 또는 위로 뚫고 나갈 수 있다.
다시 말하자면 좀 황당한 예이긴 하지만 자식요소에 z-index:-999999 를 해도 부모중에 쌓임 맥락인 부모 밑으로 내려갈 수 없다.

- 형제 요소들간의[같은 단계의] 상황에서 쌓임 순서
    - 뿌리요소인 html 요소
    - position 값이 있고 z-index 값이 음수인 요소와 그 자식요소들 ( z-index 값이 같으면 HTML 작성 순서에 따라 렌더링 )
    - position 값이 없는 요소 ( HTML 작성 순서에 따라 렌더링 )
    - position 값이 없고 opacity 값이 1보다 작은 요소
    - 그리고 position 값이 있고 z-index 값이 없거나 auto 인 요소와 그 자식요소들( 예제 파일 index2 참고 ), ( HTML 작성 순서에 따라 렌더링 )
    - position 값이 있고 z-index 값이 양수인 요소와 그 자식요소들 ( z-index 값이 같으면 HTML 작성 순서에 따라 렌더링 )


