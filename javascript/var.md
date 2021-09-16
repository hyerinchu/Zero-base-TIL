> 스코프란 변수에 접근 가능한 범위

1.  var은 함수 스코프, let은 블록 스코프를 가진다

- 즉 함수에서 var을 썼을 때는 밖에서 접근하지 못하지만
  if문, for문 안에서 썼을 때는 밖에서 접근 할 수가 있다

#

## var 사용시 문제점

<br>

```js
for (var i = 0; i < winNums.length; i++) {
  setTimeout(() => showNumbers(winNums[i], $result), 1000 * (i + 1));
}
```

- setTimeout에 전달한 콜백함수와 1000*(i+1)는 다른 시점에 실행 된다
  1000*(i+1)은 반복문을 돌 때 실행되고, 콜백함수는 지정한 시간 뒤에 호출된다. 그런데 반복문은 매우 빠른 속도로 돌아서 콜백함수가 실행될 때는 이미 i가 6으로 되어있다.

- winBalls[6]은 undefined가 된다
  console.log(winBalls[i],i)를 출력해보면 5번 모두
  undefined, 6 이 출력된다

#

### let 을 썼을 땐 왜 이런 문제가 발생하지 않았을까?

> for 문에서 쓰이는 let은 하나의 블록마다 i가 고정된다 (블록 스코프의 특성) 따라서 setTimeout의 콜백 함수 내부의 i도 setTimeout을 호출할 때의 i와 같은 값이 들어간다

#

### 만약 var을 쓰고 싶다면?

- 함수안에 가둬준다 function은 i 를 전달받고 매개변수에 등록해준다

- 그래서 j는 함수안에 갇히게 된다. j는 그때그때의 i를 가리키게 된다.

```
for (var i = 0; i < lottos.length; i++) {
  (function (j) {
    setTimeout(() => {
      showBall(lottos[j], $result);
    }, 1000 * (j + 1));
  })(i);
}

```

> 클로저란 ? 함수와 함수 바깥에 있는 변수와의 관계
> 함수와 함수 바깥에 있는변수를
> 함수와 함수 안에 있는 변수로 바꿔서 문제를 해결하였다.

> 반목문과 var을 쓸 때 항상 스코프 관련 문제가 생기는 것은 아니나 비동기가 함수와 반복문, var을 만나면 클로저 문제가 발생한다

> 출처 Let's get it 자바스크립트
