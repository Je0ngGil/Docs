### 삽입 정렬 알고리즘
삽입 정렬은 두 번째 요소부터 시작하여 끝 요소까지 차례대로 기준하여, 기준 왼측의 정렬된 배열에 알맞은 자리를 찾아 삽입하는 알고리즘이다.   
정렬된 배열에 자리를 찾아가기 때문에 이미 정렬된 배열에 대해선 *배열안에 요소끼리 교환*이 발생하지 않고,자 리를 찾기 위한 *요소 비교*도 한번씩 발생하므로 O(N)의 시간복잡도를 가진다.   
구현 자체도 다른 정렬 알고리즘에 비해 단순하지만, 정렬하려는 배열이 역순으로 배치된 상황에서는 *배열안에 요소끼리 교환*과 *요소 비교*이 최대로 발생하여 O(N^2)의 시간복잡도를 가지게 된다.

### 문제 링크
https://onlinejudge.u-aizu.ac.jp/courses/lesson/1/ALDS1/1/ALDS1_1_A

### JavaScript 풀이
```js
const input = require('fs').readFileSync('./dev/stdin', 'UTF-8').toString().split('\n');

const N = +input[0];
const sequence = input[1].split(' ').map((str) => +str);

function solution(N, sequence, compareFunc) {
  const result = [sequence.join(' ')];

  for (let i = 1; i < N; i++) {
    const key = sequence[i];

    for (let j = i - 1; j >= 0; j--) {
      if (compareFunc(key, sequence[j])) {
        swapArrayElement(sequence, j, j + 1);
      } else {
        break;
      }
    }

    result.push(sequence.join(' '));
  }

  return result.join('\n');
}

function swapArrayElement(arr, idx1, idx2) {
  const temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}

console.log(solution(N, sequence, (base, other) => base < other));

```
