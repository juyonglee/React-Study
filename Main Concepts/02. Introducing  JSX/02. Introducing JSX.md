# Introducing JSX
아래의 재미있는 Tag 구문은 String도 HTML도 아니다.
```JavaScript
const element = <h1>Hello, Wolrd</h1>;
```
## Why JSX?
- React는 rendering logic이 다른 UI 로직과 본질적으로 결합되어 있다는 사실을 포함한다. (이벤트 처리 방법, 시간 경과에 따른 상태 변경 방법 및 데이터 표시 준비 방법)
- JSX를 꼭 사용할 필요가 없지만 JavaScript 코드 내에서 UI 작업할 때 유용하고 오류 및 경고 메시지를 쉽게 확인할 수 있으므로 가급적 JSX를 사용해라.


## Embedding Expressions in JSX
JSX에서는 **{ }** 안에 JavaScript Expression을 넣을 수 있다.
### [Example 01]
```JavaScript
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
);
```
### [Example 02]
```JavaScript
function formatName(user) {
    return user.firstNAme + ' ' + user.lastName;
}

const user = {
    firstName: 'Juyong',
    lastName: 'Lee'
};

const element = <h1>Hello, {formatName(user)}</h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
);
```

## JSX is an Expression Too
- 컴파일 후 JSX 표현식은 일반 JavaScript 함수 호출과 JavaScript 객체로 평가됩니다.
- 즉, 변수 할당, if 문 및 for 루프 안에서 JSX를 사용할 수 있다.
```JavaScript
function getGreeting(user) {
    if(user) {
        return <h1>Hello, {formatName(user)}!</h1>;
    }
    return <h1>Hello, Stranger.</h1>;
}
```

## Specifying Attributes with JSX
- 따옴표를 사용하여 string literals을 속성으로 지정할 수 있습니다.
    ```JavaScript
    const element = <div tabIndex="0"></div>;
    ```
- 중괄호를 사용하여 속성에 JavaScript 표현식을 포함시킬 수도 있습니다.
- 속성에 JavaScript 표현식을 사용할 때 중괄호를 따옴표로 묶지 마십시오.
    ```JavaScript
    const element = <img src={user.avatarUrl}></img>;
    ```
    
`[Warning]` JSX는 HTML보다 JavaScript에 가깝기 때문에 React DOM은 HTML attribute 이름 대신 camelCase 규칙을 사용합니다.

## Specifying Children with JSX
JSX tags Children을 가질 수 있다.
```JavaScript
const element = (
    <div>
        <h1>Hello!</h1>
        <h2>Good to see you here.</h2> 
    </div>
);
```
