### 최대 공약수 (GCD)

공약수는 주어진 정수들을 나누어 나머지가 0인 정수를 말한다.

최대 공약수는 공약수 중 가장 큰 값을 말한다.

최대 공약수를 구하는 방법은 유클리드 호제법을 이용하면 편하다.

유클리드 호제법은 두 정수의 최대 공약수를 쉽게 구하는 방법이다.

기본 아이디어는 a와 b의 최대 공약수는 b와 a (mod) b의 최대 공약수와 같다는 것이다.

### 문제 링크
https://onlinejudge.u-aizu.ac.jp/courses/lesson/1/ALDS1/1/ALDS1_1_B

### JavaScript 구현

```js
const input = require('fs').readFileSync('./dev/stdin', 'UTF-8').toString().split('\n');

const [a, b] = input[0].split(' ').map(Number);

function solution(a, b) {
  return b === 0 ? a : solution(b, a % b);
}

console.log(solution(a, b));
```

GCD 재귀 함수를 반복하다보면 b값이 0이 된다.

한 정수를 0으로 나눈 나머지는 그대로이므로 재귀 함수의 탈출 조건이 된다.

더 나아가 두 정수 뿐만아니라 여러 정수의 최대공약수를 구하는 코드를 구현해봤다.

```js
function GCDInNumberArray(nums) {
  // 1. nums의 0이 아닌 가장 작은 수를 찾는다.
  const minNum = Math.min(...nums.filter((num) => num));

  // 2. 1에서 찾은 가장 작은 정수를 mod에서 제외시킬 map 배열이다.
  const numsMap = nums.map((num) => minNum === num);

  // 3. 2의 map 배열을 토대로 b를 제하고, x mod b를 모든 원소에 적용한다.
  const dividedNums = nums.map((num, idx) => (numsMap[idx] ? num : num % minNum));

  // 4. 0과 minNum을 걸러낸다.
  const numsOtherThanZeroOrMinNum = dividedNums.filter((num) => num && num !== minNum);

  // 5. numsOtherThanZeroOrMinNum의 길이가 0이라면 dividedNums은
  // [0, 0, minNum, minNum, ...] 로 구성되어 있으므로 재귀 함수의 탈출 조건이 된다.
  if (numsOtherThanZeroOrMinNum.length === 0) return minNum;
  else return GCDInNumberArray(dividedNums);
}
```
위 코드를 간략히 정리하자면

a, b, c, d, e의 최대 공약수를 구할 때, GCDInNumberArray(\[a, b, c, d, e])

1. 가장 작은 정수를 찾는다. (b가 가장 작은 정수라고 가정)
2. 배열에 b인 경우와 0인 경우를 제하고 모든 원소에 mod b를 적용한다. (\[a % b, b, c % b, d % b, e % b])
3. 모든 원소가 가장 작은 정수와 같아지거나 0이 된다면 가장 작은 정수가 최대 공약수이다.
4. 다시 \[a % b, b, c % b, d % b, e % b]로 1, 2를 반복한다.
 
