### 문제 링크
https://onlinejudge.u-aizu.ac.jp/courses/lesson/1/ALDS1/1/ALDS1_1_A

### 알고리즘
삽입 정렬 알고리즘
...

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
