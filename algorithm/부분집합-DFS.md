> 자연수 N이 주어지면 1부터 N까지의 원소를 갖는 집합의 부분집합 모두 출력하시오 (공집합 제외)

N = 3일 때 {1,2,3}의 부분집합을 공집합을 제외하고 출력해야 한다

경우의 수로 생각하면 쉬운데 부분집합의 총 갯수는

1 -> 존재 할 수도 존재하지 않을수도 (2가지 경우의 수)

2 -> 존재 할 수도 존재하지 않을수도 (2가지 경우의 수)

2 -> 존재 할 수도 존재하지 않을수도 (2가지 경우의 수)

2 x 2 x 2 (공집합 포함이다)

#

### 트리형태로 나타내기

<br>

![
](https://images.velog.io/images/chuhyerin96/post/ce59b264-c185-48f5-a28a-f2a6f27eab25/%E1%84%87%E1%85%AE%E1%84%87%E1%85%AE%E1%86%AB%E1%84%8C%E1%85%B5%E1%86%B8%E1%84%92%E1%85%A1%E1%86%B8%20%E1%84%90%E1%85%B3%E1%84%85%E1%85%B5.jpeg)

#

## DFS 코드로 표현하기

```js
function solution(number) {
  const answer = [];
  const check = Array.from({ length: number + 1 }, () => 0);

  function DFS(L) {
    if (L === number + 1) {
      let set = "";
      check.forEach((number, index) => {
        if (number === 1) set += index + " ";
      });
      if (set.length > 0) answer.push(set.trim());
    } else {
      check[L] = 1;
      DFS(L + 1);
      check[L] = 0;
      DFS(L + 1);
    }
  }
  DFS(1);
  return answer;
}

console.log(solution(4));
```

> 1.  check이라는 배열을 만들고 길이는 number+1, 모든 요소는 0으로 초기화 시켜준다
> 2.  check 배열은 0과 1로만 이루어 질 것인데 1은존재, 0은 존재하지 않음을 의미한다
> 3.  check의 길이를 주어진 숫자보다 1크게 설정한 것은 index를 사용할 것이고 0번 index는 사용하지 않을 것이기 때문이다
>
> - 1번인덱스가 0이면 부분집합에 1이라는 숫자가 없다는 의미
> - 2번인덱스가 1이면 부분집합에 2라는 숫자기 있다는의미
>
> 4.  `L===number+1 `일 때 종료시켜주고
>     1인 경우에만(index숫자가 있다는 의미) index를 더해주어 >부분집합을 만든 뒤 answer에 push 해준다
> 5.  공집합인 경우는 제외해야 하니 길이가 0보다 큰 경우에만 정답배열에 push 해준다

### 코드의 핵심

```js
check[L] = 1;
DFS(L + 1);
check[L] = 0;
DFS(L + 1);
```

이 부분이 재귀함수의 핵심부분인데 처음에 트리를 보고,스택프레임이 어떻게 진행되는지 return 한 뒤 어디로 돌아가는지 적어보면서 이해하는 것이 좋다

#

## 처음 작성한 코드

```js
function solution(number) {
  const answer = [];
  const tem = Array.from({ length: number }, () => 0);
  const numbers = Array.from({ length: number }, (v, i) => i + 1);
  console.log(numbers);
  function DFS(L) {
    if (L === number) {
      let set = "";
      for (let x of tem) {
        if (x !== 0) set += x + " ";
      }
      if (set.length > 0) answer.push(set.trim());
      return;
    } else {
      tem[L] = numbers[L];
      DFS(L + 1);
      tem[L] = 0;
      DFS(L + 1);
    }
  }
  DFS(0);
  return answer;
}
```

index를 활용한다는 것을 생각하지 못해서 numbers라는 배열을 또 만들었다

결국 핵심은 숫자가 있냐 없냐를 기준으로 트리를 뻗어나가는 것이다

#

> 출처 자바스크립트 알고리즘 문제풀이
