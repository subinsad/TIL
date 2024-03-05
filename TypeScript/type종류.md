### 문자

```tsx
let str : string
let red : string = “Red”
let green : string = ‘green’
let myColor : string = ‘My color is ${red}.’
let yourColor : string = ‘Your color is’ + green
```

### 숫자

```tsx
let num: number;
let integer: number = 6;
let float: number = 3.14;
let infinity: number = Infinity;
let nan: number = NaN;
```

### 불린

```tsx
let isBoolean: boolean;
let isDone: boolean = false;
```

### Null / Undefined

```tsx
let null : null
let und : undefined
console.log(null) // 값을 할당하지 않아서 에러발생
console.log(und)
```

### 배열

<aside>
💡 배열을 의미하는 대괄호와 그 안에 들어갈 아이템의 타입을 같이 작성해야 함

</aside>

```tsx
const fruits : string[] = ['Apple', 'Banana', 'Cherry']
const numbers : number[] = [1, 2, 3, 4, 5, 6, 7]
const union : {string | number)[] = ['Apple', 1, 2, 'Banana', 3]
```

### 객체

<aside>
💡 인터페이스에 작성한 속성만 사용가능함, 속성을 추가할 수 없음

</aside>

```tsx
const obj = object = {}
const arr : object = []
const func : object = function (){}

const userA : {
	name : string
	age : number
	isValid : boolean
} = {
	name : 'Heropy'
	age : 85,
	isValid : true
}
```

-   user 인터페이스 생성

```tsx
interface User{
// 파스칼케이스로 사용하여 일반변수와 구분함
	name : string
	age : number
	isValid : boolean
}

const userA : User {
	name : 'Heropy'
	age : 85,
	isValid : true
}

const userB : User {
	name : 'subin'
	age : 20,
	isValid : false
}
```

### 함수

```tsx
const add : **(x : number, y : number) => number** = function(x,y) {
	return x + y
}
const a : number = add(1,2)

const hello : () => void = function () {
	console.log('Hello world')
}
const h : void = hello()
```

-   변경가능 : 중간에 타입을 명시하는 것이 없더라도 함수 자체에서 매개변수 혹은 반환하는
    데이터 타입을 명시할 수 있다.

```tsx
const add : function(x : **number** ,y: **number**): **number** {
	return x + y
}

const hello = function () : **void** {
	console.log('Hello world')
}
```

### Any

-   아무거나 변수의 데이터 타입으로 사용할 수 있다.

```tsx
let hello: any = 'Hello';
hello = 123;
hello = false;
hello = null;
hello = {};
hello = [];
hello = function () {};
```

### UnKnown

-   알 수가 없는 상태이다.
-   any type보다 엄격하고 조건을 따져서 가능하거나 가능하지 않은 상황을 코드상에서 알려줌

```tsx
const a: any = 123;
const u: unknown = 123;

const any: any = a;
const boo: boolean = a;
const num: number = a;
const arr: string[] = a;
const obj: { x: string; y: number } = a;
```

### Tuple

-   배열데이터와 유사함

```tsx
const tuple: [string, number, boolean] = ['a', 1, false];
const users: [number, string, boolean][] = [
    [1, 'Neo', true],
    [2, 'Evan', false],
    [3, 'Lewis', true],
];
```

### Void

-   return 키워드를 명시하지 않은 함수에서 반환되는 타입

```tsx
function hello(msg: string): void {
    console.log(`Hello ${msg} `);
}
const hi: void = hello('world');
```

### Never

-   절대 발생하지 않을

```tsx
const nev: [] = [];
nev.push(3);
```

### Union

-   동시에 여러개 타입을 사용할 때 사용

```tsx
let union: string | number;
union = 'Hello type!';
union = 123;
union = false; // err
```

### Intersection

-   객체타입을 합쳐서 & 기호를 사용해서 사용

```tsx
interface User {
    name: string;
    age: number;
}
interface Validation {
    isValid: boolean;
}
const heropy: User & validation = {
    name: 'Neo',
    age: 85,
    isValid: true,
};
```
