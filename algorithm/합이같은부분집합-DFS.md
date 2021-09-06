> 문제 : 집합이 주어졌을 때 서로소인 두 부분집합의 합이 같은 경우가 있으면
> YES 없으면 NO를 출력해라

```js
function solution(numbers) {
  let answer = "NO";
  let set = Array.from({ length: numbers.length }, (v) => 0);
  let flag = 0;
  const total = numbers.reduce((pre, cur) => pre + cur, 0);
  function DFS(L) {
    if (flag) return;
    if (L === numbers.length) {
      const setSum = set.reduce((pre, cur) => pre + cur, 0);

      if (total - setSum === setSum) {
        flag = 1;
        return (answer = "YES");
      }
      return;
    } else {
      set[L] = numbers[L];
      DFS(L + 1);
      set[L] = 0;
      DFS(L + 1);
    }
  }
  DFS(0);
  return answer;
}
```

집합으로 [1, 3, 5, 6, 7, 10]가 주어졌을 때 모든 수가 들어있는집합과 공집합 부터 비교를 시작한다

합에 관련된 것이므로 두개중 하나의 부분집합의 합만 구하면 된다 즉,

- `total - setSum === setSum` 만 판별해 주면 된다
  재귀함수 밖에 부분집합을 정의해 두었고 주어진 집합의 원소의 갯수만큼 0으로 초기화 시켜주었다

#### flag변수를 사용해 준 이유는 합이 같은 경우를 찾아도 스택프레임에 아직 재귀함수들이 남아 있기때문에 바로바로 종료시켜주기 위한 것이다

### 하지만 위의 코드는 비효율적이고 2개의 매개변수를 사용하는 것이 좋다

#

## 개선된 코드

```js
function solution(numbers) {
  let answer = "NO";
  let flag = 0;
  const total = numbers.reduce((pre, cur) => pre + cur, 0);
  function DFS(L, sum) {
    // if (flag) return;
    if (L === numbers.length) {
      if (total - sum === sum) {
        flag = 1;
        return (answer = "YES");
      }
      return;
    } else {
      DFS(L + 1, sum + numbers[L]);
      DFS(L + 1, sum);
    }
  }
  DFS(0, 0);
  return answer;
}
```

> - DFS(0,0)에서 첫번째 인자는 index라고 생각하면 편할 것 같다
> - L+1일 때 L번째 index에 대해 처리를 해준다
> - `L+1===numbers.length`일 때 멈추는 이유는
>   주어진 배열.length 가 5라고 가정하면 DFS(5)가 됬을 때 배열의 마지막 index인 4를 처리해 주기 때문이다
