## Set

- Set은 ES6부터 추가된 자료구조 중 하나다.
- Set은 유일한 값을 갖는 집합(set)을 나타내는 자료구조 유사하다.
- Set은 내부적으로 해시 테이블(Hash Table)로 구현되어 있으며, 값이 추가되는 방식과 검색 속도 등에서 이점을 가진다.

<br />

### Set vs Array

Set 객체는 배열과 유사하지만 다음과 같은 차이가 있다.

| 구분                                | 배열 | Set 객체 |
| :---------------------------------- | ---- | :------- |
| 동일한 값을 중복하여 포함할 수 있다 | O    | X        |
| 요소 순서에 의미가 있다             | O    | X        |
| 인덱스로 요소에 접근할 수 있다      | O    | X        |

- Set은 내부적으로 삽입 순서 유지하지만, Set은 순서를 기준으로 요소에 직접적인 접근을 제공하지는 않는다.

---

### Set 객체의 생성

- Set 생성자 함수 `Set()`을 이용해서 생성 할 수 있다.
- Set 생성자 함수에 인수를 전달하지 않으면 빈 Set 객체가 생성된다.

```javascript
const set = new Set();

console.log(set); // Set(0) {}
```

- Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.

```javascript
// string을 인수로 전달
const set = new Set('apple');

console.log(set); // Set(4) { 'a', 'p', 'l', 'e' }
```

```javascript
// number를 인수로 전달
const set = new Set(9);

console.log(set); // TypeError: number 9 is not iterable (cannot read property Symbol(Symbol.iterator))
```

```javascript
// 배열을 인수로 전달
const set = new Set([1, 2, 3, 4, 5, 6]);

console.log(set); // Set(6) { 1, 2, 3, 4, 5, 6 }
```

```javascript
// 객체를 인수로 전달
const set = new Set({ name: 'ashley', age: '23' });

console.log(set); // TypeError: object is not iterable (cannot read property Symbol(Symbol.iterator))
```

<br />

### Set.prototype.size 프로퍼티

- `size` 접근자 속성은 Set 객체의 요소 개수를 반환한다.

```javascript
const set = new Set([1, 2, 3, 3]);

console.log(set.size); // 3
```

- getter 함수만 존재하는 접근자 프로퍼티다.

```javascript
const set = new Set([1, 2, 3]);
console.log(set.size); // 3
console.log(Object.getOwnPropertyDescriptor(Set.prototype, 'size'));
/*
{
  get: [Function: get size],
  set: undefined,
  enumerable: false,
  configurable: true
}
*/

set.size = 10; // 무시
console.log(set.size); // 3
```

- Array의 `length`는 변경 할 수 있다.

<br />

### Set.prototype.add 메서드

- Set 객체에 요소를 추가하고 싶을 때 사용한다.

```javascript
const set = new Set();
console.log(set); // Set(0) {}

set.add(1);
console.log(set); // Set(1) { 1 }
```

- `add` 메서드는 새로운 요소가 추가된 Set 객체를 반환한다. 그래서 add 메서드를 호출한 후에 add 메서드를 연속적으로 호출할 수 있다.

```javascript
const set = new Set();

set.add(1).add(2).add('hi').add('i').add('am').add('set');
console.log(set); // Set(6) { 1, 2, 'hi', 'i', 'am', 'set' }
```

- `add` 매서드는 새로운 요소가 추가된 Set 객체를 반환하기 때문에 변수에 할당할 수 있다.

```javascript
const set = new Set();
set.add(1).add(2);

const set2 = set.add(3);
console.log(set2); // Set(3) { 1, 2, 3 }
console.log(set); // Set(3) { 1, 2, 3 }

// 같은 참조 값을 가진다
console.log(set === set2); // true
```

- Set 객체에 중복된 요소의 추가는 허용되지 않는다. 중복된 값을 추가하면 에러가 발생하지 않고 무시된다.

```javascript
const set = new Set();
set.add(1).add(2).add(2);

console.log(set); // Set(2) { 1, 2 }
```

- Set 객체는 객체나 배열과 같이 자바스크립트의 모든 값을 요소로 저장할 수 있다.

```javascript
const set = new Set();
set
  .add(1)
  .add('a')
  .add(false)
  .add(undefined)
  .add(null)
  .add({})
  .add([])
  .add(() => {});

console.log(set);
/* 
Set(8) {
  1,
  'a',
  false,
  undefined,
  null,
  {},
  [],
  [Function (anonymous)]
}
*/
```

- Set에 Set을 추가할 수 있다.

```javascript
const set = new Set();
const obj1 = { value: 1, number: 1 };
const set2 = new Set([1, 2, 3, 3, 4]);

set.add(obj1).add(set2);

console.log(set); // Set(2) { { value: 1, number: 1 }, Set(4) { 1, 2, 3, 4 } }
```

- 객체 타입은 참조 값이 같은 경우에만 중복 취급을 한다.

```javascript
// 참조 값이 다른 경우
const set = new Set();

const obj1 = { value: 1, number: 1 };
const obj2 = { value: 1, number: 1 };

set.add(obj1).add(obj2);

console.log(set);
// Set(2) { { value: 1, number: 1 }, { value: 1, number: 1 } }
```

```javascript
// 참조 값이 같은 경우
const set = new Set();

const obj1 = { value: 1, number: 1 };
const obj2 = obj1;

set.add(obj1).add(obj2);

console.log(set); // Set(1) { { value: 1, number: 1 } }
```

- Set 객체는 `NaN`과 `NaN`을 같다고 평가하여 중복 추가를 허용하지 않는다. `+0`과 `-0`도 마찬가지다.

```javascript
const set = new Set();
console.log(NaN === NaN); // false;
console.log(0 === -0); // true;

// NaN과 NaN을 같다고 평가
set.add(NaN).add(NaN);
console.log(set); // Set(1) { NaN }

// +0과 -0을 같다고 평가한다
set.add(0).add(-0);
console.log(set); // Set(1) { NaN, 0 }
```

---

### SameValue 알고리즘

**SameValueZero**

1. If `Type(x)` is different from `Type(y)`, return `false`.
2. If `Type(x)` is `Number`, then
   - If x is `NaN` and y is `NaN`, return `true`.
   - If x is `+0` and y is `-0`, return `true`.
   - If x is `-0` and y is `+0`, return `true`.
   - If x is the same `Number` value as y, return `true`.
   - Return `false`.
3. Return `SameValueNonNumber(x, y)`.

**SameValueNonNumber**

1. Assert: `Type(x)` is not Number.
2. Assert: `Type(x)` is the same as `Type(y)`.
3. If `Type(x)` is `Undefined`, return `true`.
4. If `Type(x)` is `Null`, return `true`.
5. If `Type(x)` is `String`, then
   1. If `x` and `y` are exactly the same sequence of code units (same length and same code units at corresponding indices), return `true`; otherwise, return `false`.
6. If `Type(x)` is `Boolean`, then
   1. If `x` and `y` are both `true` or both `false`, return `true`; otherwise, return `false`.
7. If `Type(x)` is `Symbol`, then
   1. If `x` and `y` are both the same `Symbol` value, return `true`; otherwise, return `false`.
8. Return `true` if `x` and `y` are the same `Object` value. Otherwise, return `false`.

---

### Set.prototype.has 메서드

- Set 객체에 특정 요소가 존재하는지 확인할 때 사용한다.
- `has` 메서드는 특정 요소의 존재 여부를 `Boolean` 값으로 반환한다.

```javascript
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true
console.log(set.has('a')); // false
```

<br />

### Set.prototype.delete 메서드

- `delete` 메서드는 삭제 성공 여부를 나타내는 `Boolean` 값을 반환한다.
- 삭제하려는 요소값을 인수로 전달해야 한다. 만약 요소가 존재하지 않는다면 에러 없이 무시된다.

```javascript
const set = new Set([1, 2, 3]);
set.delete(2);
console.log(set); // Set(2) { 1, 3 }

const deleted = set.delete(7);
console.log(deleted); // false
```

- `add` 메서드와 다르게 Set 객체가 아닌 `Boolean` 값을 반환하기 때문에 연속적으로 호출할 수 없다.

```javascript
const set = new Set([1, 2, 3]);

set.delete(1).delete(2); // TypeError: set.delete(...).delete is not a function
```

<br />

### Set.prototype.clear 메서드

- Set 객체의 모든 요소를 일괄 삭제할 수 있다.
- `clear` 메서드는 언제나 `undefined`를 반환한다.

```javascript
const set = new Set([1, 2, 3]);

set.clear();
console.log(set); // Set(0) {}
```

<br />

### Set.prototype.entries 메서드

- Set 객체의 각 요소를 `[value, value]` 형태의 배열로 순회할 수 있는 Iterator 객체를 반환한다.

```javascript
const set = new Set([1, 2, 3]);
const iterator = set.entries();

console.log(iterator.next()); // { value: [ 1, 1 ], done: false }
console.log(iterator.next()); // { value: [ 2, 2 ], done: false }
console.log(iterator.next()); // { value: [ 3, 3 ], done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

<br />

### Set.prototype.values() 메서드

- Set 객체의 각 요소 값을 순회하는 Iterator 객체를 반환한다.

```javascript
const set = new Set();
set.add('apple');
set.add('banana');
set.add('orange');

const keys = set.values();
console.log(values.next()); // { value: "apple", done: false }
console.log(values.next()); // { value: "banana", done: false }
console.log(values.next()); // { value: "orange", done: false }
console.log(values.next()); // { value: undefined, done: true }
```

<br />

### Set.prototype.keys() 메서드

- Set 객체의 각 요소의 키 값을 순회하는 Iterator 객체를 반환한다.
- `keys` 메서드는 `values` 메서드의 별칭이다.

```javascript
const set = new Set();
set.add('apple');
set.add('banana');
set.add('orange');

const keys = set.keys();
console.log(keys.next()); // { value: "apple", done: false }
console.log(keys.next()); // { value: "banana", done: false }
console.log(keys.next()); // { value: "orange", done: false }
console.log(keys.next()); // { value: undefined, done: true }
```

<br />

### Set.prototype.forEach 메서드

- 첫 번째 인수: 현재 순회 중인 요소값
- 두 번째 인수: 현재 순회 중인 요소값
- 세 번째 인수: 현재 순회 중인 Set 객체 자체

\* 첫 번째 인수와 두 번째 인수가 같은 값인 이유는 `Array.prototype.forEach`와 통일하기 위함이다.

```javascript
const set = new Set([1, 2, 3, 4, 5, 6]);

set.forEach((value, value2, set) => {
  console.log(value, value2, set);
});

/*
1 1 Set(6) { 1, 2, 3, 4, 5, 6 }
2 2 Set(6) { 1, 2, 3, 4, 5, 6 }
3 3 Set(6) { 1, 2, 3, 4, 5, 6 }
4 4 Set(6) { 1, 2, 3, 4, 5, 6 }
5 5 Set(6) { 1, 2, 3, 4, 5, 6 }
6 6 Set(6) { 1, 2, 3, 4, 5, 6 }
*/
```

<br />

### for ... of

```javascript
const set = new Set([1, 2, 3, 4, 5, 6]);

for (const value of set) {
  console.log(value);
}

/*
1
2
3
4
5
6
*/
```

<br />

### Spread 문법

```javascript
const set = new Set([1, 2, 3, 4, 5, 6]);

// set -> array
console.log([...set]); // [1, 2, 3, 4, 5, 6]
```

<br />

### Destructuring

```javascript
const set = new Set([1, 2, 3, 4, 5, 6]);

const [a, ...rest] = set;
console.log(a, rest); // 1, [2, 3, 4, 5, 6]
```

---

### 중복 제거

- 중복을 허용하지 않는 Set 객체의 특성을 활용하여 배열에 중복된 요소 제거 가능하다.
- 배열의 중복 요소 제거

```javascript
const array = [2, 1, 2, 3, 4, 3, 4];
const unique = array.filter((value, index, self) => self.indexOf(value) === index);
console.log(unique); // [2, 1, 3, 4]

// filter: O(n), indexOf: O(n) => O(n^2)
```

- Set을 사용한 배열의 중복 제거

```javascript
const array = [2, 1, 2, 3, 4, 3, 4];
const unique = [...new Set(array)]; // O(n) + O(n) = O(2n) -> O(n)

console.log(unique); // [2, 1, 3, 4]
```

<br />

### 두 배열 사이의 공통적 요소들 확인

```javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = [2, 4, 6, 8];
const commonValues = new Set(arr1.filter((num) => arr2.includes(num)));

console.log(commonValues); // Output: Set(2) { 2, 4 }
```

---

### 교집합

- 집합 A와 집합 B의 공통 요소로 구성

```javascript
// option 1
Set.prototype.intersection = function (set) {
  const result = new Set();

  for (const value of set) {
    if (this.has(value)) result.add(value);
  }

  return result;
};

// option 2
Set.prototype.intersection = function (set) {
  return new Set([...this].filter((value) => set.has(value)));
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

console.log(setA.intersection(setB)); // Set(2) { 2, 4 }
console.log(setB.intersection(setA)); // Set(2) { 2, 4 }
```

<br />

### 합집합

- 집합 A와 집합 B의 중복 없는 모든 요소로 구성된다

```jsx
// option 1
Set.prototype.union = function (set) {
  const result = new Set(this);

  for (const value of set) {
    result.add(value);
  }

  return result;
};

// option 2
Set.prototype.union = function (set) {
  return new Set([...this, ...set]);
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

console.log(setA.union(setB)); // Set(4) { 1, 2, 3, 4 }
console.log(setB.union(setA)); // Set(4) { 2, 4, 1, 3 }
```

<br />

### 차집합

- 집합 A에는 존재하지만 집합 B에는 존재하지 않는 요소로 구성된다

```jsx
// option 1
Set.prototype.difference = function (set) {
  const result = new Set(this);

  for (const value of set) {
    result.delete(value);
  }

  return result;
};

// option 2
Set.prototype.difference = function (set) {
  return new Set([...this].filter((value) => !set.has(value)));
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

console.log(setA.difference(setB)); // Set(2) { 1, 3 }
console.log(setB.difference(setA)); // Set(0) {  }
```

<br />

### 부분 집합과 상위 집합

- 집합 A가 집합 B에 포함되는 경우 집합 A는 집합 B의 부분 집합이며, 집합 B는 집합 A의 상위 집합이다.

```javascript
// option 1
Set.prototype.isSuperset = function (subset) {
  for (const value of subset) {
    if (!this.has(value)) return false;
  }

  return true;
};

// option 2
Set.prototype.isSuperset = function (subset) {
  const supersetArr = [...this];
  return [...subset].every((value) => supersetArr.includes(value));
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

console.log(setA.isSuperset(setB)); // true
console.log(setB.isSuperset(setA)); // false
```
