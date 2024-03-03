<aside>
<b> 💡 useEffect( () ⇒ {} )  : 렌더링이 될때 실행
useEffect ( () ⇒ { } , [] ) : 화면에 첫 렌더링 될때

</aside>

```js
function App() {
    const [count, setCount] = useState(1);
    const [name, setName] = useState('');

    const click = () => {
        setCount(count + 1);
    };

    const handleInput = (e) => {
        setName(e.target.value);
    };
    //렌더링될때마다 매번 실행됨 - 렌더링 이후
    useEffect(() => {
        console.log('렌더링');
    });

    // 마운팅 + count가 변화할때마다 실행
    useEffect(() => {
        console.log('렌더링');
    }, [count]);

    // 마운팅 + name이 변경될때마다 실행
    useEffect(() => {
        console.log('렌더링');
    }, [name]);

    // 마운팅
    useEffect(() => {
        console.log('렌더링');
    }, []);

    return (
        <>
            <div>
                <span> 현재 시각 : {count} </span>
                <button onClick={click}> update </button>
                <input type="text" value={name} onChange={handleInput} />
                <span> name:{name} </span>
            </div>
        </>
    );
}
```
