8장. 함수
 함수 정의하기
  - 함수 선언문으로 정의
     function square(x) { return x*x; }
    함수 리터럴로 정의
     var square = function(x) { return x*x; }
     // 함수 리터럴로 정의한 함수는 그 참조를 변수에 할당한 후에 호출 가능
     console.log(square(2));    // ->4
    Function생성자로 정의
     var square = new function("x", "return x*x);
     // Function 생성사로 정의한 함수는 그 참조를 변수에 할당한 후에 호출 가능
     console.log(square(2));    // ->4
    화살표 함수 표현식으로 정의
     var square = x => x*x;
     // 화살표 함수 표현식으로 정의한 함수는 그 참조를 변수에 할당한 후에 호출 가능
     console.log(square(2));    // ->4
  - 중첩 함수: 특정 함수의 내부에 선언된 함수
     함수 안의 if, while문 등 내부에는 사용불가
     외부함수의 바깥에서는 읽고 쓰기 불가
     자신을 둘러싼 외부 함수의 인수와 지역변수에 접근 가능
 함수 호출하기
  - 함수 호출
     var s = square (5);
    메서드 호출
     obj.m = function() { ... };
     obj.m();
    생성자 호출
     var obj = new Object();
    call, apply를 통한 간접 호출
  - 즉시 실행 함수: 익명 함수를 정의하고 곧바로 실행함
     (function() { ... })();
     (function() { ... }());
     (function(a, b) { ... })(1, 2);
     즉시 실행 함수에도 이름을 붙일 수 있지만 함수 내부에서만 이름이 유효
 함수의 인수
  - 호출할 때 인수를 생략할 수 있는 함수
    함수 정의식에서 인수를 생략했을 때(undefined) 사용할 초깃값 설정!
    function multiply(a, b)
    {
        b = b || 1; //초깃값이 1
        return a*b;
    }
    multiply(2, 3); // ->6
    multiply(4)     // -> 4
    ||: 왼쪽 피연산자가 true로 평가되면 왼쪽 피연산자를 반환. 
        왼쪽 피연산자가 false로 평가되면 오른쪽 피연산자를 반환.
        b에 인수를 전달하면 true로 평가되어 b값을 그대로 사용
        아니면 b= undefined이므로 false로 평가되어 초깃값을 사용
 Arguments 객체
     arguments 객체? 함수에 전달된 인수에 해당하는 Array형태의 객체. 
     "유사 배열 객체"
     arguments.length: 인수 개수
     arguments.callee: 현재 실행중인 함수의 참조
     argument[i]값을 바꾸면 i+1번째 인자의 값이 함께 바뀜
     function f(x, y)
     {
        arguments[1] = 3;
        console.log("x =" + x + ", y =" +y);
     }
     f(1, 2);   // -> x=1, y=3
     위 코드에서 arguments[1]값을 바꾸면 함수의 인자 y값이 함께 바뀜
     var params = [].slice.call(arguments); :유사배열객체를 배열 객체로 변환
 재귀 함수
     : 자기 자신을 호출하는 함수
     arguments.callee를 사용해 이름 없는 익명 함수를 재귀호출하기
     var fact = function(n)
     {
        if(<=1>) return 1;
        return n*atguments.callee(n-1);
     }
   - 1) 재귀 호출은 반드시 멈춰야 한다
     2) 재귀 호출로 문제를 간단하게 해결할 수 있을 때만 사용한다.
        웬만하면 while, for문으로 작성하는것이 좋음
 this 값
     : 함수가 호출되었을 때 그 함수가 속해 있던 객체의 참조
      실행 문맥의 대스 바인딩 컴포넌트가 참조하는 객체
     var tom = {
        name: "Tom",
        sayHello: function(){
            console.log("Hello! " + this.name);
        }
     };
     tom.sayHello(); //-> 함수의 참조. Hello! Tom
     this값이 가리키는 객체가 tom이므로 this.name값은 Tom
     var huck = { name: "Huck" };
     huck.sayHello = tom.sayHello;
     huck.sayHello();    //-> Hello! Huck
     실행 문맥의 디스 바인딩 컴포넌트가 가리키는 객체가 huck로 바뀜
  -  1)최상위 레벨 코드의 this
        전역 객체
     2)이벤트 처리기 안에 있는 this
        이벤트가 발생한 요소 객체를 가리킴
     3)생성자 함수 안에 있는 this
        그 생성자로 생성한 객체
     4)생성자의 prototype 메서드 안에 있는 this
        그 생성자로 생성한 객체
     5)직접 호출한 함수 안에 있는 this
        함수 앞에 어떤 객체를 붙여서 호출하면 디스 바인딩 컴포넌트가 그 객체를 가리킴
        var a = {};
        a.f = f;    //디스 바인딩 컴포넌트가 a가리킴
        a.f();      
     6)apply와 call 메서드로 호출한 함수 안에 있는 this
        this가 가리키는 ㅐㄱ체를 바꿀 수 있음
 클로저
     : 자기 자신이 정의된 환경에서 함수 안에 있는 자유변수의 식별자 결정을 실행하는 자료 구조의 모음
     캡슐화된 객체
  -  외부 함수 호출 
      -> 함수의 렉시컬 환경 컴포넌트 생성 ( 외부 함수가 호출될 때 마다 생성, 중첩 함수의 함수 객체가 있는 한 삭제되지 않음. 함수 객체가 사라져도 삭제되지 않음. ) 
      ->함수 내부 중컵함수의 함수 객체를 생성해서 반환 
      -> 외부함수의 렉시컬 환경 컴포넌트를 참조하는 중첩함수가 정의한 클로저 생성 (외부함수는 클로저를 생성하는 팩토리 함수)
     클로저 내부 상태는 은폐되어 있고, 중첩 함수 안에서만 읽고 쓸 수 있음(캡슐화)
 이름 공간
  - 전역 유효 범위 오염: 전역 변수와 전역 함수를 전역 객체에 선언
    오염 방지 기법
    1) 객체를 이름 공간으로 활용
       이름 공간: 변수 이름과 함수 이름을 한곳에 모아 이름 충돌을 미리 방지하고, 변수와 함수를 쉽게 가져다 쓸 수 있는 메커니즘
       객체를 값으로 가지는 전역 변수 생성 - 그 객체에 프로그램 전체에서 사용하는 모든 변수와 함수를 프로퍼티로 정의
       var myApp = myApp || {};
       myApp.name = "Tom";
       myApp.showName = function(){ ... };
       ...
       마이앱 객체에 전역 유효 범위에서 사용하고자 하는 모든 변수와 함수를 프로퍼티로 추가하면 오염 최소화 가능
    2) 함수를 이름 공간으로 활용
        라이브러리를 읽어 들여 사용할 때 라이브러리 안에 있는 전역 변수와 충돌하지 않게 하려면 전체 프로그램을 즉시함수 안에 넣어서 실행
        (function(){//이곳에 프로그램 작성})();
 객체로서의 함수
  - 자바스크립트의 객체는 일급 객체
    일급 객체인 함수는 일급 함수
  - 함수의 프로퍼티
    caller  
    length 
    name
    prototype

    apply(): 선택한 this와 인수를 사용해 함수 호출. 인수는 배열 객체
    bind(): 선택한 this와 인수를 적용한 새로운 함수 반환
    call(): 선택한 this와 인수를 사용해 함수 호출. 인수는 쉼표로 구분한 값
    constructor: Function생성자의 참조
    toString(): 함수의 소스코드를 문자열로 만들어 반환