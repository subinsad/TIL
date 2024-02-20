## 1. 컴포넌트 안에서 쓰는 if/else

```js
function Component() {
    if (true) {
        return <p>참일경우 </p>;
    } else {
        return null;
    }
}
```

-   보통 return + JSX 전체를 포함하는 if문을 작성
-   이 경우에는 else 생략이 가능함

## 2. JSX안에서 쓰는 삼항연산자

<b> 조건문 ? 조건문 참일때 실행할 코드 : 거짓일때 실행할 코드 </b>

```js
function Component() {
    return <div>{1 === 1 ? <p> 참일때 보여줄 코드 </p> : null}</div>;
}
```

-   jsx내에서 if/else 대신에 사용할 수 있음.
-   if와 다르게 JSX안에서도 실행 가능함.
-   중첩사용도 가능함

## 3. && 연산자로 if 역할 대신하기

<b> 자바스크립트의 &&연산자</b>

-   왼쪽 오른쪽 둘 다 true면 전체를 true로 변경

```js
true && false;
true && true;
```

-   맨 위의 코드는 그 자리에 false가 남음
-   밑 코드는 true가 남음
-   만약 false를 넣는게 아니라 자료형을 넣으면 '안녕'을 넣을경우 안녕이 남는다.

```js
function Component(){
   return (<div>{1 === 1 ? <p> 참일때 보여줄 코드 </p> : null}</div>;
    )
}

function Component(){
    return (
    <div>{1 === 1 && <p>참이면 보여줄 html</p>;}</div>
    )
}
```

-   위 두개는 동일한 역할

## 4. switch / case 조건문

-   if문이 중첩해서 여러개 달려있는 경우에 사용

```js
function Component2() {
    var user = 'seeller';
    switch (user) {
        case 'seeller':
            return <h4>판매자로그인</h4>;
        case 'customer':
            return <h4>구매자 로그인 </h4>;
        default:
            return <h4>그냥로그인</h4>;
    }
}
```

1. switch(검사할변수){} 작성
2. 그 안에 case 검사할 변수와 일치하냐 : 추가
3. 일치한다면 case 밑에있는 코드실행
4. default : 맨 마지막에 쓰는 else문과 동일함

-   if문을 연달아쓸 때 코드가 약간 줄어들 수 있지만, 변수 하나만 검사할 수 있다는 단점

## 5. object / array 자료형 응용

```js
var Ui = {
    info : <p>info</p>,
    shipping : <p>shipping</p>
    refund : <p>refund</p>
}

function Component(){
    var 현재상태 = 'info'
    return(
        <div>
            {
                Ui[현재상태]
            }
        </div>
    )
}
```

-   만약에 var 현재상태가 'info'일경우 저장된 <p>태그가 보임
-   refund상태면 저장되있는 p태그가 보임
