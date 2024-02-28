# useState

### 기본적인 state 사용법

```jsx
function App() {
    const [count, setCount] = useState(1);
    const click = () => {
        let newTime;
        if (count >= 12) {
            newTime = 1;
        } else {
            newTime = count + 1;
        }
        setCount(newTime);
    };
    return (
        <>
            <div>
                <span> 현재 시각 : {count} </span>
                <button onClick={click}> update </button>
            </div>
        </>
    );
}
```

## 세부내용

```jsx
const heaveWork = () => {
  return ['홍길동', '김민수'];
};

function App() {
  const [names, setNames] = useState(() => {
    return heaveWork();
  });
  const [input, setInput] = useState('');

  const handleInput = (e) => {
    setInput(e.target.value); // input에 작성한 값을 setInput에 넣기
  };
  console.log(input);

  const handleUpload = () => {
    setNames((prevState) => { // 이전의 값
      return [input, ...prevState]; // 작성한값과 이전의 값
    });
  };
  return (
    <>
      <input type="text" value={input} onChange={handleInput} />
      <button onClick={handleUpload}>upload</button>
      {names.map((name, idx) => {
        return <p key={idx}> {name} </p>;
      })}
    </>
  );
```

### 입력

input에 입력한 값이 버튼을 누르면 map으로 뿌려진다.

### 출력

내용을 입력하세요.

<aside>
💡 const [state, setState] = setState(초기값);

</aside>

-   setState는 값이 변경될때마다 리렌더링이 된다. 만약 초기값이 변경된다면? 계속 리렌더링이 발생
    > 초기값에 콜백함수를 넣어 함수를 작성해주면 1번만 실행되어 처음에 한번만 동작함
-   input에 작성한 값을 setInput에 넣어준다 : setInput(e.target.value)
-   btn을 누르면 작성한 값이 보이게 한다 : handleUpload함수에 이름이 바뀌는함수인 setNames에
    이전의값을 매개변수로 넣고, return할때 작성한 값과 이전에 작성한값이 보이게 처리한다.

---
