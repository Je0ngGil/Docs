### 문제 링크
https://onlinejudge.u-aizu.ac.jp/courses/lesson/1/ALDS1/1/ALDS1_1_C

### JavaScript 구현
```js
const input = require('fs').readFileSync('/dev/stdin', 'UTF-8').toString().split('\n');

const intArray = input.map(Number);

function solution(intArray) {
  let result = 0;
  // intArray의 원소에는 중복된 정수가 있고, 결과에서 중복된 정수를 제하여 소수의 개수를 구해야 한다.
  const intSet = new Set(intArray);

  for (const int of intSet) {
    if (isPrimeNumber(int)) result++;
  }

  return result;
}

function isPrimeNumber(num) {
  if (num <= 1) return false;
  if (num <= 3) return true;

  if (num % 2 === 0 || num % 3 === 0) return false;

  // 아래 첨부된 사진을 보면
  // 소수는 6n을 기준으로 6n - 1 또는 6n + 1에 분포한다. (n은 자연수)
  // 따라서 반복문의 증감식은 6의 배수로 증가하고,
  // 조건식은 num의 제곱근을 초과해서 체크하는 것은 무의미하므로 아래와 같이 구현한다.
  for (let i = 5; i * i <= num; i += 6) {
    if (!(num % i && num % (i + 2))) return false;
  }

  return true;
}

console.log(solution(intArray));

```

![image](https://github.com/Je0ngGil/Docs/assets/127815742/7dabd04d-f73e-4e0b-ab52-b0a8d872f02a)

