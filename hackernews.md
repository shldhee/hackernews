* `fecth()` : 모든 브라우저가 fetch API를 지원하는 것은 아닙니다.
* 이전 절에서 fetch API로 해커 뉴스 데이터를 받아왔습니다. 하지만 모든 브라우저가 fetch API를 지원하는 것은 아닙니다. 특히 오래된 브라우저는 fetch API를 지원하지 않으며, 헤드리스 브라우저(Headless Browser)에서 애플리케이션을 테스트할 때, fetch API와 관련된 문제가 발생할 수 있습니다. 헤드리스 브라우저는 실제 애플리케이션이 구동되는 브라우저가 아닌 테스트용으로 테스트 자동화에 사용되는 브라우저입니다. 물론 구버전 브라우저(폴리필, polyfill)와 테스트(isomorphic-fetch)에서도 fetch API를 사용할 수 있는 방법이 있지만, 이 책에서는 이 내용을 다루지 않겠습니다.
[https://developer.mozilla.org/ko/docs/Web/API/Fetch_API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API)
* `superagent`
* `axios`
* 지금부터 fetch() 메서드 대신 axios() 메서드를 사용하겠습니다. 사용법은 fetch API와 거의 동일합니다. 인자는 URL이며 프로미스(promise)를 반환합니다. 반환된 응답을 JSON으로 변환하지 않아도 됩니다. axios 이 일을 하며. 자바스크립트에서 data 객체로 반환합니다. 따라서 반환된 데이터 구조 그대로 사용하면 됩니다.
* `if (result === null)` 대신 축약 표기법인 `if (!result)`
* `Object.assign()`

* 배열 스프레드 연산자

``` js
const userList = ['Robin', 'Andrew', 'Dan'];
const additionalUser = 'Jordan';
const allUsers = [ ...userList, additionalUser ];

console.log(allUsers);
// 출력: ['Robin', 'Andrew', 'Dan', 'Jordan']
//
result: Object.assign({}, this.state.result, { hits: updatedHits })
result: { ...this.state.result, hits: updatedHits }
```

* 객체 스프레드 연산자

``` js
const userNames = { firstname: 'Robin', lastname: 'Wieruch' };
const age = 28;
const user = { ...userNames, age };

console.log(user);
// 출력: { firstname: 'Robin', lastname: 'Wieruch', age: 28 }
```

* && 연산자

``` js
const result = true && 'Hello World';
console.log(result);
// 출력: Hello World

const result = false && 'Hello World';
console.log(result);
// 출력: false

애플리케이션에도 적용해봅시다. 조건이 참이면, && 논리 연산자 뒷부분 내용이 출력됩니다. 조건이 거짓이면 리액트는 표현식을 무시하고 이를 건너뜁니다. 이번에도 조건이 참이면 Table 컴포넌트를 반환하고 거짓이면 반환하지 않게 만들어봅시다.

{ result &&
  <Table
    list={result.hits}
    pattern={searchTerm}
    onDismiss={this.onDismiss}
  />
}
```

* 고차 컴포넌트 : HOCs는 여러 사용 사례가 있습니다. 프로퍼티 준비, 상태 관리, 컴포넌트 표시 변경을 할 수 있습니다. 또는 조건부 렌더링에서 HOCs를 헬퍼로 사용할 수 있습니다. 예를 들어 List 컴포넌트가 있는데, 이 컴포넌트는 리스트를 반환하거나 리스트가 없거나 null일 경우 아무것도 반환하지 않는다고 합니다. HOCs는 리스트가 없을 때 렌더링 하지 못하게 할 수 있습니다. 이렇게 하면 List 컴포넌트는 리스트가 없을 경우를 체크하지 않아도 됩니다. 그저 List 컴포넌트는 리스트를 렌더링 하는 역할에만 충실하면 됩니다.