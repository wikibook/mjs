# 04-01

```javascript
10 + 20
```

# 04-02

```javascript
// 변수는 하나의 값을 저장하기 위한 수단이다.
var userId = 1;
var userName = 'Lee';

// 객체나 배열 같은 자료구조를 사용하면 여러 개의 값을 하나로 그룹화해서 하나의 값처럼 사용할 수 있다.
var user = { id: 1, name: 'Lee' };

var users = [
  { id: 1, name: 'Lee' },
  { id: 2, name: 'Kim' }
];
```

# 04-03

```javascript
var result = 10 + 20;
```

# 04-04

```javascript
var score; // 변수 선언(변수 선언문)
```

# 04-05

```javascript
console.log(score); // undefined

var score; // 변수 선언문
```

# 04-06

```javascript
var score;  // 변수 선언
score = 80; // 값의 할당
```

# 04-07

```javascript
var score = 80; // 변수 선언과 값의 할당
```

# 04-08

```javascript
console.log(score); // undefined

var score;  // ① 변수 선언
score = 80; // ② 값의 할당

console.log(score); // 80
```

# 04-09

```javascript
console.log(score); // undefined

var score = 80;     // 변수 선언과 값의 할당

console.log(score); // 80
```

# 04-10

```javascript
console.log(score); // undefined

score = 80; // 값의 할당
var score;  // 변수 선언

console.log(score); // ??
```

# 04-11

```javascript
var score = 80; // 변수 선언과 값의 할당
score = 90;     // 값의 재할당
```

# 04-12

```javascript
var person, $elem, _name, first_name, val1;
```

# 04-13

```javascript
var 이름, なまえ;
```

# 04-14

```javascript
var first-name; // SyntaxError: Unexpected token –
var 1st;        // SyntaxError: Invalid or unexpected token
var this;       // SyntaxError: Unexpected token this
```

# 04-15

```javascript
var firstname;
var firstName;
var FIRSTNAME;
```

# 04-16

```javascript
var x = 3;       // NG. x 변수가 의미하는 바를 알 수 없다.
var score = 100; // OK. score 변수는 점수를 의미한다.
```

# 04-17

```javascript
// 경과 시간. 단위는 날짜다
var d;                 // NG

var elapsedTimeInDays; // OK
```

# 04-18

```javascript
// 카멜 케이스 (camelCase)
var firstName;

// 스네이크 케이스 (snake_case)
var first_name;

// 파스칼 케이스 (PascalCase)
var FirstName;

// 헝가리언 케이스 (typeHungarianCase)
var strFirstName; // type + identifier
var $elem = document.getElementById('myId'); // DOM 노드
var observable$ = fromEvent(document, 'click'); // RxJS 옵저버블
```
