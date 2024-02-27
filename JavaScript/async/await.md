# 이론

### 제너레이터란?

-   ES6에서 도입된 제너레이터 코드는 코드 블록의 실행을 일시 중지했다가 필요한 시점에
    재개할 수 있는 특수한 함수
-   제너레이터 함수는 화살표 함수로 정의할 수 없다.
-   new연산자와 함께 생성자 함수로 호출할 수 없다.

### 제너레이터 객체

<aside>
💡 제너레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라 제너레이터 객체를
생성해 반환한다. 제너레이터 함수가 반환한 객체는 iterable(이터러블)이면서 동시에 iterator(이터레이터)이다.

</aside>

---

## async / await

<aside>
💡 제너레이터를 사용해서ㅣ동기 처리를 동기 처리처럼 동작하도록 구현했지만, 코드가 장황해지고 가독성이 나빠짐, 그래서 간단하고 가독성 좋게 비동기 처리를 동기처리처럼 동작할수 있도록 구현할 수 있는 **async / await가 도입**

</aside>

### async

-   await 키워드는 반드시 async 함수 내부에서 사용해야 함
-   async함수는 async 키워드를 사용해 정의하며 언제나 프로미스를 반환함
-   async함수가 명시적으로 프로미스를 반환하지 않더라도 async 함수는 암묵적으로 반환값을
    resolve하는 프로미스를 반환

```jsx
// 함수 선언문
async function foo(n) {return n;}
foo(1).then(v => console.log(v)); //1

// 함수 표현식
const bar = async function (n) {return n;);
bar(2).then(v => console.log(v)); //2

// 화살표 함수
const baz = async n => n;
bar(3).then(v => console.log(v)); // 3

// 메서드
const obj = {
	async foo(n) P return n;}
};
obj.foo(4).then(v => console.log(v)); // 4

// 클래스 메서드
class MyClass {
	async bar(n) {return n;}
}
const myClass = new MyClass();
myClass.bar(5).then( v => console.log(v)) //5
```

<aside>
💡 클래스의 constructor 메서드는 async 메서드가 될 수 없다.
클래스의 constructor 메서드는 **인스턴스를 반환**해야 하지만, async 함수는 **언제나 프로미스**를 반환

</aside>

-   **Promise**는 다음 세 가지 상태 중 하나일 수 있다.
    -   **Pending**: Fulfilled도 Rejected도 아닌 초기 상태.
    -   **Fulfilled**: 작업이 성공적으로 완료되었으며 약속이 값으로 해결됩니다.
    -   **Rejected**: 작업이 실패했으며 Promise가 이유나 오류로 인해 거부되었습니다.

## await 키워드

-   프로미스가 settled(비동기 처리가 수행된 상태) 가 될때까지 대기
-   settled 상태가 되면 프로미스가 resolve한 처리 결과를 반환
-   await 키워드는 반드시 프로미스 앞에서 사용

```jsx
async function foo() {
    const a = await new Promise((resolve) =>
        setTimeout(() => resolve(1), 3000)
    );
    const b = await new Promise((resolve) =>
        setTimeout(() => resolve(2), 2000)
    );
    const c = await new Promise((resolve) =>
        setTimeout(() => resolve(3), 1000)
    );

    console.log([a, b, c]); // [1,2,3]
}
foo(); // 약 6초 소요
```

-   모든 프로미스에 await 키워드를 사용하는 것은 주의해야 한다.
-   foo 함수 종료될때까지 약 6초가 소요된다.
-   그런데 foo함수가 수행하는 3개의 비동기 처리는 **서로 연관이 없이 개별적으로 수행되는 비동기 처리**이므로
    앞선 비동기 처리가 완료될 때까지 대기해서 순차적으로 처리할 필요가 없다. (아래코드로 수정)

```jsx
async function foo(){
	const res = await Promise.all([
		new Promise(resolve => setTimeout(() => resolve(1),3000));
		new Promise(resolve => setTimeout(() => resolve(2),2000));
		new Promise(resolve => setTimeout(() => resolve(3),1000));

	console.log(res); // [1,2,3]
}
foo() // 약 3초 소요
```

---

-   앞선 비동기 처리의 결과를 가지고 다음 비동기 처리를 수행해야 한다.
    따라서 비동기 처리의 **처리 순서가 보장**되어야 하므로 모든 프로미스에 await 키워드를 써서 순차적으로 처리할 수 밖에 없다.

```jsx
async function foo(n) {
    const a = await new Promise((resolve) =>
        setTimeout(() => resolve(n), 3000)
    );
    //두번째 비동기 처리를 수행하려면 첫 번째 비동기 처리 결과가 필요
    const b = await new Promise((resolve) =>
        setTimeout(() => resolve(a + 1), 2000)
    );
    // 세번째 비동기 처리를 수행하려면 두 번째 비동기 처리 결과가 필요
    const c = await new Promise((resolve) =>
        setTimeout(() => resolve(b + 1), 1000)
    );

    console.log([a, b, c]); // [1,2,3]
}
foo(1); // 약 6초 소요
```

## 에러처리

<aside>
💡 **try … catch문 사용**

</aside>

-   콜백함수를 인수로 전달받는 비동기 함수와 달리 프로미스를 반환하는 비동기 함수는
    명시적으로 호출할 수 있기 때문에 호출자가 명확함

```jsx
const fetch = require('node-fetch');

const foo = async () => {
	try {
		const wrongUrl = 'https://wrong.url';

		const response = await fetch(wrongUrl);
		const data = await response.json();
		console.log(data);
	} catch(err)
			console.log(err); // TypeError : failed to fetch
	}
}
foo();
```

-   HTTP통신에서 발생한 네트워크 에러뿐 아니라 try 코드 블록 내의 모든문에서 발생한 일반적인 에러까지 캐치
-   **async함수 내에서 catch 문을 사용해서 에러 처리를 하지 않으면 async 함수는 발생한 에러를
    reject하는 프로미스를 반환한다.**
