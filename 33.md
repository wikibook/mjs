# 33-01

```javascript
// Symbol 함수를 호출하여 유일무이한 심벌 값을 생성한다.
const mySymbol = Symbol();
console.log(typeof mySymbol); // symbol

// 심벌 값은 외부로 노출되지 않아 확인할 수 없다.
console.log(mySymbol);        // Symbol()
```

# 33-02

```javascript
new Symbol(); // TypeError: Symbol is not a constructor
```

# 33-03

```javascript
// 심벌 값에 대한 설명이 같더라도 유일무이한 심벌 값을 생성한다.
const mySymbol1 = Symbol('mySymbol');
const mySymbol2 = Symbol('mySymbol');

console.log(mySymbol1 === mySymbol2); // false
```

# 33-04

```javascript
const mySymbol = Symbol('mySymbol');

// 심벌도 레퍼 객체를 생성한다
console.log(mySymbol.description); // mySymbol
console.log(mySymbol.toString());  // Symbol(mySymbol)
```

# 33-05

```javascript
const mySymbol = Symbol();

// 심벌 값은 암묵적으로 문자열이나 숫자 타입으로 변환되지 않는다.
console.log(mySymbol + ''); // TypeError: Cannot convert a Symbol value to a string
console.log(+mySymbol);     // TypeError: Cannot convert a Symbol value to a string
```

# 33-06

```javascript
const mySymbol = Symbol();

// 불리언 타입으로는 암묵적으로 타입 변환된다.
console.log(!!mySymbol); // true

// if 문 등에서 존재 확인을 위해 사용할 수 있다.
if (mySymbol) console.log('mySymbol is not empty.');
```

# 33-07

```javascript
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로운 심벌 값을 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 있으면 해당 심벌 값을 반환
const s2 = Symbol.for('mySymbol');

console.log(s1 === s2); // true
```

# 33-08

```javascript
// 전역 심벌 레지스트리에 mySymbol이라는 키로 저장된 심벌 값이 없으면 새로운 심벌 값을 생성
const s1 = Symbol.for('mySymbol');
// 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출
Symbol.keyFor(s1); // -> mySymbol

// Symbol 함수를 호출하여 생성한 심벌 값은 전역 심벌 레지스트리에 등록되어 관리되지 않는다.
const s2 = Symbol('foo');
// 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출
Symbol.keyFor(s2); // -> undefined
```

# 33-09

```javascript
// 위, 아래, 왼쪽, 오른쪽을 나타내는 상수를 정의한다.
// 이때 값 1, 2, 3, 4에는 특별한 의미가 없고 상수 이름에 의미가 있다.
const Direction = {
  UP: 1,
  DOWN: 2,
  LEFT: 3,
  RIGHT: 4
};

// 변수에 상수를 할당
const myDirection = Direction.UP;

if (myDirection === Direction.UP) {
  console.log('You are going UP.');
}
```

# 33-10

```javascript
// 위, 아래, 왼쪽, 오른쪽을 나타내는 상수를 정의한다.
// 중복될 가능성이 없는 심벌 값으로 상수 값을 생성한다.
const Direction = {
  UP: Symbol('up'),
  DOWN: Symbol('down'),
  LEFT: Symbol('left'),
  RIGHT: Symbol('right')
};

const myDirection = Direction.UP;

if (myDirection === Direction.UP) {
  console.log('You are going UP.');
}
```

# 33-11

```javascript
// JavaScript enum
// Direction 객체는 불변 객체이며 프로퍼티는 유일무이한 값이다.
const Direction = Object.freeze({
  UP: Symbol('up'),
  DOWN: Symbol('down'),
  LEFT: Symbol('left'),
  RIGHT: Symbol('right')
});

const myDirection = Direction.UP;

if (myDirection === Direction.UP) {
  console.log('You are going UP.');
}
```

# 33-12

```javascript
const obj = {
  // 심벌 값으로 프로퍼티 키를 생성
  [Symbol.for('mySymbol')]: 1
};

obj[Symbol.for('mySymbol')]; // -> 1
```

# 33-13

```javascript
const obj = {
  // 심벌 값으로 프로퍼티 키를 생성
  [Symbol('mySymbol')]: 1
};

for (const key in obj) {
  console.log(key); // 아무것도 출력되지 않는다.
}

console.log(Object.keys(obj)); // []
console.log(Object.getOwnPropertyNames(obj)); // []
```

# 33-14

```javascript
const obj = {
  // 심벌 값으로 프로퍼티 키를 생성
  [Symbol('mySymbol')]: 1
};

// getOwnPropertySymbols 메서드는 인수로 전달한 객체의 심벌 프로퍼티 키를 배열로 반환한다.
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(mySymbol)]

// getOwnPropertySymbols 메서드로 심벌 값도 찾을 수 있다.
const symbolKey1 = Object.getOwnPropertySymbols(obj)[0];
console.log(obj[symbolKey1]); // 1
```

# 33-15

```javascript
// 표준 빌트인 객체를 확장하는 것은 권장하지 않는다.
Array.prototype.sum = function () {
  return this.reduce((acc, cur) => acc + cur, 0);
};

[1, 2].sum(); // -> 3
```

# 33-16

```javascript
// 심벌 값으로 프로퍼티 키를 동적 생성하면 다른 프로퍼티 키와 절대 충돌하지 않아 안전하다.
Array.prototype[Symbol.for('sum')] = function () {
  return this.reduce((acc, cur) => acc + cur, 0);
};

[1, 2][Symbol.for('sum')](); // -> 3
```

# 33-17

```javascript
// 1 ~ 5 범위의 정수로 이루어진 이터러블
const iterable = {
  // Symbol.iterator 메서드를 구현하여 이터러블 프로토콜을 준수
  [Symbol.iterator]() {
    let cur = 1;
    const max = 5;
    // Symbol.iterator 메서드는 next 메서드를 소유한 이터레이터를 반환
    return {
      next() {
        return { value: cur++, done: cur > max + 1 };
      }
    };
  }
};

for (const num of iterable) {
  console.log(num); // 1 2 3 4 5
}
```
