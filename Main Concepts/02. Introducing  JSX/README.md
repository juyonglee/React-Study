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

# JSX Prevents Injection Attacks
사용자 입력을 JSX에 내장하는 것은 안전합니다.
```JavaScript
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```
- ReactDOM는 JSX를 렌더링 하기전에 기본적으로 공격에 사용될 수 있는 위험한 요소들을 제거한다. 
- 모든 것은 렌더링되기 전에 문자열로 변환됩니다. 
- 이를 통해 Injection 공격에 대한 별다른 설계없이 간편하게 React를 사용할 수 있으며 XSS (cross-site-scripting) 공격을 예방하는 장점이 있다.

# JSX Represents Objects
- Babel은 JSX를 React.createElement() 호출로 컴파일합니다.
- 아래의 두 예제는 동일합니다.
    ### [Example 01]
    ```JavaScript
    const element = (
        <h1 className="greeting">
            Hello, world!
        </h1>
    );
    ```
    ### [Example 02]
    ```JavaScript
    const element = React.createElement(
        'h1',
        {className: 'greeting'},
        'Hello, world!'
    );
    ```
- React.createElement()는 bug-free한 코드를 작성하는 데 도움이되는 몇 가지 검사를 수행하지만 기본적으로 다음과 같은 객체를 만듭니다.
    ```JavaScript
    // Note: this structure is simplified
    const element = {
        type: 'h1',
        props: {
            className: 'greeting',
            children: 'Hello, world!'
        }
    };
    ```
- 이러한 객체들을 “React elements”라고 한다.
- React는 이러한 객체를 읽고 이를 사용하여 DOM을 구성하고 최신 상태로 유지합니다.

### `[TIP]`
ES6 및 JSX 코드가 올바르게 강조 표시되도록 선택한 편집기에 "Babel"언어 정의를 사용하는 것이 좋습니다. 이 웹 사이트는 호환 가능한 [Oceanic Next](https://labs.voronianski.com/oceanic-next-color-scheme/) 색 구성표를 사용합니다.
