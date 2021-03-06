# Javascript-repository
Javascript 지식
====

script를 body맨 뒤에 삽입하는 이유.
----   
html과 css가 먼저 렌더링이 되어야 하는데 script부분이 중간에 끼게 되면 렌더링을 방해할 수 있기 때문.    
이는 사용자 입장에서 완성되지 않은 화면을 오랫동안 볼 수가 있어서 좋지 않다.   

script가 head에 있는 경우. 
----   
웹이 script에 의존적일 때 head에 넣을 수 있다.    
이 경우에는 async와 defer를 사용하는데 이는 script부분을 만났을 때 html,css를 파싱하면서 같이 다운로드하는 식이다.    
async와 defer의 차이점을 보자면 async는 결국 파싱도중에 script가 다운이 다 된다면 그땐 멈춰서 실행하고 defer는 다운로드만 받아놓는 식이다. 그래서 defer로 통일하는 게 좋아보인다.   
ex) ```<script defer src=“script.js”>```   

var, const, let은 언제? 
-----
var는 변수를 중복해서 사용할 수 있는데 이는 오히려 기존에 선언해 둔 변수의 존재를 잊고 재할당 할 수도 있어 위험이 있다.    
이를 보완하여 나온 게 let, const이다. 이들은 변수가 중복되면 에러가 나서 중복해서 사용할 수 없게 만든다. 또한 var는 함수레벨스코프이고 let, const는 블록레벨스코프이기 때문에 var타입을 사용할 때 for문과 같은 부분에서 유의해서 작성할 필요가 있다.    

이벤트 버블링, 이벤트 캡처, 이벤트 위임이란?
-----
이벤트 버블링은 하위의 이벤트가 상위로 전파되는 것. 세 개의 이벤트가 등록되었을 때 가장 하위의 이벤트가 실행될 때 상위 이벤트까지 전파되어 실행된다.   
이벤트 캡처는 상위의 이벤트가 하위로 전파되는 것.    
이벤트 위임은 상위 요소만 이벤트를 등록하면 하위의 이벤트로 버블링이 되는 것. 상위요소에서 요소가 추가되거나 삭제될 때 쉽게 제어할 수 있다는 점이 장점이다.   

클로저란?
-----
외부 함수의 실행이 끝나고 외부 함수가 소멸된 이후에도 내부 함수가 외부 함수의 변수에 접근할 수 있는 구조를 클로저라고 부른다.   
클로저가 필요한 이유는       
1. 전역변수를 줄일 수 있다.     
2. 비슷한 형태의 코드를 재사용할 수 있다.    
3. 정보의 은닉이 필요하다고 느낄 때 사용한다.    

이벤트루프에 대해서
-----
자바스크립트는 단일스레드 기반이지만 NodeJS, 브라우저기반에서는 동시성을 지원하게 된다.     
이는 이벤트루프와 큐테스크가 있기 떄문인데 이벤트루프는 콜스택에 아무런 작업이 없을 때 비동기API를 큐테스크에 넣는다. 그리고 호출스택이 빌 때마다 큐테스크에서 작업을 가져와 실행하게 한다.     
결론적으로 모든 비동기 API들은 작업이 완료되면 콜백 함수를 태스크 큐에 넣고, 이벤트 루프는 현재 실행중인 테스크가 없을 때 테스크 큐의 첫 번째를 가져와 실행하게된다. 이는 동시성을 지원한다고 볼 수 있다.    

프로토타입에 대해서
------
자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있다. 이는 연결해서 사용하는 것이기에 객체지향의 상속 개념처럼 사용할 수 있는데 이러한 부모 객체를 프로토타입이라고 한다.     
이렇게 생성된 객체의 proto에는 조상 프로토타입의 링크가 있기에 조상의 객체속성과 메소드를 사용할 수가 있다.    

프로토타입의 장단점에 대해서
-----
프로토타입 위주의 프로그래밍을 한다면 자식객체에서 부모객체에 접근해서 사용할 수 있기에 유연한 프로그래밍이 가능하다고 볼 수 있다. 하지만 클래스기반의 언어처럼 상위에서 정의해놓은 것을 그대로 따르는 게 아닌 역방향이 가능하기에 정확성과 안전성 측면에서 떨어질 것이다.    
    
호이스팅에 대해서
-----
호이스팅은 자바스크립트에서 함수가 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언하는 것 같이 보이는 것이다. 이는 var 변수 선언문과 함수선언문에서 일어난다.    
유의할 점은 var변수 선언과 함수선언이 동시에 일어나게 된다면 var변수가 먼저 호이스팅이 일어난 뒤에 함수선언이 일어나기에 그 사이에 호출이 있다면 이는 undefined가 될 수 있다. 즉 변수 선언이 함수 선언보다 우선순위가 높다는 것이다.      

호이스팅을 만든 이유에 대해서
----    
var타입으로 정의해서 코드의 문맥이 맞지 않더라도 에러가 아닌 undefined를 노출시키는 게 장점으로 보일 수도 있겠지만 사람마다 생각하는 게 다른 것 같다.    

실행 컨텍스트에 대해서
-----    
실행 가능한 코드를 형상화하고 구분하는 추상적인 개념, 실행 가능한 코드가 실행되기 위해 필요한 환경으로 변수 객체, scope chain, this로 구성된다. 간단하게 원칙을 보자면 이렇다.
1. 전연 컨텍스트 하나 생성 후, 함수 호출 시마다 컨텍스트 생성    
2. 컨텍스트 생성 시 컨텍스트 안에 변수객체, scope, chain, this 생성    
3. 함수 실행 시 변수가 객체 안에서 없다면 스코프 체인을 따라 찾음.    
4. 함수가 끝나면 해당 컨텍스트가 사라지고 페이지가 종료되면 전역 컨텍스트가 사라짐.    

== vs ===
-----
a==b는 a와 b가 같은지만 확인하고 ===은 데이터 타입까지 비교해서 같으면 true 아니면 false를 보낸다. 이는 숫자타입일 때고 배열일 때는 값이 같더라도 변수가 다르다면 주소값이 다르게 참조돼 ==와 ===상황 둘 다 false의 결과를 보게 된다.(객체도 마찬가지)    
    


setTimeout(callback, 0)의 실행원리
-----
setTimeOut함수의 두 번째 인자인 0ms초만큼 지난 후에 태스크 큐에 추가한다. 그리고 이후 콜스택에 있는 태스크들이 전부 종료되면 태스크 큐에 있던 첫 번째 테스크를 이벤트 루프가 가져와 실행한다.     

콜백함수는?
----    
콜백함수는 함수를 나중에 호출하는 것인데, 이를 통해 비동기적인 프로그래밍을 할 수 있다.     

Promise란? async await이란?
----    
Promise는 자바스크립트 비동기 처리에 사용되는 객체이다. 이는 데이터를 불러오기도 전에 화면에 데이터를 표시할 때 빈 화면을 보여줄 수 있기 때문에 사용한다. promise에는 체이닝 개념이 존재하는데 이는 비동기 데이터를 유연하게 값을 가공할 수 있어 함수형 프로그래밍에서 유용하게 쓰인다.    

async await에 대해서
-----
async await문법은 promise와 콜백함수의 단점을 보완하려고 만든 문법으로 보다 직관적으로 비동기 프로그래밍을 할 수 있다. 또한 계속해서 return하는 형식의 Promise와는 달리 await async만 붙임으로써 데이터를 받아올 때까지 기다렸다가 원하는 시점에 사용할 수 있다.    

ES6 추가문법 몇가지
----
1. Arrows 함수 = function보다 구문이 짧고 자신의 this, arguments를 바인딩 하지않는다.    
2. Classes의 생성 = 객체지향패턴을 더 쉽게 사용할 수 있게 됨.    
3. 구조분해할당 = 배열이나 객체의 속성을 해체하여 개별적인 변수를 담는 방식    
4. let, const = 변수선언방법으로 해당타입으로 정의된 변수는 중복으로 나타날 수 없다.     
5. iterators, For...of : 반복에 대한 편의성 제공.    
    


NULL 병합 연산자 ‘??’
----
??를 통해 해당 값이 null인지 undefined를 검사하고 둘 중 하나가 맞다면 다른 의도하는 값을 출력시킬 수 있다.    
예시로 a ?? b라면 a가 null도 undefined도 아니면 a 아니면 b를 출력한다.    
조금 깊게 || 연산자와의 차이점을 보자면 ||는 0까지도 포용할 수 있다는 것이다.     
ex)    
```let width = 0;```    
```alert(width ?? 100);```   
```alert(width || 100);```
    
??의 경우에는 null이거나 undefined일 때가 아니라면 width를 출력하게 되고, ||의 경우에는 0이거나 null이거나 undefined일 때 100을 출력하게 된다.        
    
optional chaining
-------
.chaining operator랑 비슷하게 사용하는데 ?를 붙임으로써 그 속성이 존재하는 경우에만 chaining을 하고 아니면 undefined를 반환한다. 이의 장점은 에러를 반환하는 것이 아닌 undefined를 반환해 다른 로직들은 실행될 수 있도록 하는 것이 장점으로 볼 수 있다.    

for of 반복문의 로직
-----
[Symbol.iterator]속성을 가지고 있는 이터러블에 대해서만 사용할 수 있으며 iterator를 반환하면서 계속 도는 구조이다.    

iterable vs iterator
-----
iterable은 객체의 맴버를 반복할 수 있는 객체이다. iterable에는 Symbol.iterator가 구현되어 있어야 한다.(그래야 반복이 가능함)    
iterator는 {value, done} 객체를 리턴하는 next()를 가진 값이다.    

this에 대해
-----
this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다.    
this는 어떤 위치에 있냐, 어디에서 호출하냐, 어떤 함수에 있느냐에 따라서 참조 값이 달라진다.    

call, apply, bind
-----
call과 apply는 this 값을 바꿔주는 함수. this값을 바꿔줘야 의도하는 데이터를 바인딩 시킬 수 있기 때문. 둘의 차이점은 apply는 call과 다르게 2번째 인자를 배열에 넣어야 한다는 것이다.
그리고 bind와의 차이점은 bind는 함수를 실행하지 않는다는 것이다. 그래서 인자를 하나만 받게된다.    

mutable vs immutable
----
mutable에는 array와 object가 있고 나머지는 immutable에 해당한다. 불변적인 값으로 다루는 이유는 성능을 향상시키거나(미래에 변화되지 않는다면) 메모리 사용을 줄이기 위함(객체 전체 복사가 아닌 객체 참조)의 이유들이 있다.    

Object.freeze, Object.seal
-----
이 두 개는 객체의 값을 변하지 못하게 만드는 것인데, 차이점은 seal에서 쓰기 가능한 속성의 값은 봉인 후에도 변경할 수 있다는 것이다.    

css animation vs js animation 
-----
css animation은 반응형이 쉽고 외부 라이브러리를 필요로 하지않는다. 또한 css 자체가 선언형이기에 어떤 요소가 애니메이션을 가져야 한다는 직관적인 표현이 가능하다.    
js animation은 css로 처기하기엔 훨씬 복잡하고 무거운 애니메이션 작업들을 효율적이고 세밀하게 다루기 위해 사용한다. 또한 브라우저 호환성 측면에서 transition/animation 속성보다 뛰어나다.    

node.js, javascript
-----
둘 다 ECMAScript Spec을 사용하지만 node.js는 server를 다룰 수 있고 javascript는 client를 다룰 수 있다.     
웹팩은 파일들을 전부 해석한 뒤 하나로 합쳐주는 것이다. 장점은 하나의 js파일에 모든 게 담겨있기 때문에 여러 URL에 요청을 보내지 않아도 된다. 즉 main.js에서 묶여져서 하나의 파일안에서 처리하기에 부하가 적고 속도도 빨라진다.    
