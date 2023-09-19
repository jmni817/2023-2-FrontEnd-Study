1장. 자바스크립트의 개요
 자바스크립트? 강력하고 유연한 알고리즘 표현 능력을 갖춘 프로그래밍 언어
 1) 인터프리터 언어
    실행 속도 up, 고기능 웹 어플을 구현할 수 있음
 2) 동적 프로토타입 기반 객체 지향 언어
    클래스가 아닌 '프로토타입'을 상속
 3) 동적 타입 언어
    변수 타입 X. 실행 도중에 데이터 타입이 동적으로 바뀔 수 있음
 4) 함수가 일급 객체(first class object)
    자바스크립트의 함수는 객체, 함수에 함수를 인수로 넘길 수 있음
    함수형 프로그래밍 가능
 5) 함수가 클로저(closure)를 정의
    클로저로 변수 은닉, 영속성 보장

2장. 프로그램의 작성법과 실행법
 자바스크립트 파일명: ~.js
 Node.js의 대화형 모드로 실행하기
 - 터미널에 $ node 입력하면 >이 나옴, 이 뒤에 코드 입력하면 실행됨
 - .editor 입력하면 프로그램 전체를 보면서 입력 가능 (편집기 모드)
 - 종료하려면 .exit
자바스크립트 기본 문법
 - 유니코드 사용
 - 대/소문자 구별
 - 문장 마지막에 세미콜론 사용(;), 세미콜론 안써도 자동으로 추가됨(but, 다음줄과 이어지고 있다고 판단되면 자동 추가 X. 웬만하면 다 붙이자)
 - 빈 문장 ';'
 
3장. 변수와 값
 변수 선언자 var
  - 자바스크립트에는 변수 타입이 없으므로 선언자가 모두 var!!
 변수 끌어올림
  - 프로그램 중간에서 변수를 선언해도 맨 앞에서 선언 된 것처럼 다른 문장 앞에 생성됨
  - console.log(x);
    var x; 
    //undefined 가 출력됨(변수가 끌어올려지므로 에러 X)
  - but, 선언과 동시에 대입하는 코드는 끌어올리기 X
    ( var x = 5 가 밑에 있었다면 끌어올려지지 않음)
 식별자(변수, 함수, 라벨 등..)의 첫 글자가 숫자일 수 없음
 식별자가 예약어와 같을 수 없음
  - 예약어
    break   case  catch class const continue debugger default  delete   do else  export   extends  false finally  for   function if import   in instanceof  new   null  return   super switch   this  throw true  try   typeof   var   void  while with  yield
 동적 타입 언어: 변수에 타입이 없음, 모든 타입의 데이터 저장 가능
 데이터 타입
  - 원시 타입 (숫자, 문자열, 논리값, 특수한 값(undefined, null), 심벌)
  - 객체 타입 (참조 타입)
  - 숫자를  64bit 부동소수점으로 표현 (double타입에 해당)
 이스케이프 시퀀스: 특정 제어 코드나 문자 표현
  - \xXX: 두자릿수 16진수 XX로 지정된 Latin-1문자
  - \uXXXX: 네자릿수 16진수 XXXX로 지정된 유니코드 문자
  - \u{XXXXXX}: 16진수 코드 포인트 XXXXXX로 지정된 유니코드 문자
  - String.raw(태그 함수)를 문장" " 앞에 붙이면 이스케이프 시퀀스 문자도 출력
 심벌: 자기 자신을 제외한 그 어떤 값과도 다른 유일무이한 값. 원시 값.
 - var sym1 = Symbol(); 로 심벌 생성
 - Symbol(" ")로 인수를 전달하면 생성된 심벌의 설명을 붙일 수 있음
 - Symbol.for(" ")를 활용해 문자열과 연결된 심벌 생성
 - Symbol.keyFor()로 심벌과 연결된 문자열 구하기
   var sym1 = Symbol.for("jmni_hhh");
   console.log(Symbol.keyFor(sym1));
   // "jmni_hhh"가 출력됨
 플레이스 홀더 &{ }
 - 홀더 안에 든 부분을 표현식으로 간주하여 평가
 - console.log('오늘은 ${now.getMonth() + 1}월 ${now.getDate()}일 입니다.');
   //홀더 안에 든 부분이 평가되어 문자열로 바뀜

4장. 객체와 배열, 함수의 기초
 객체 리터럴
  - {이름: "값"}
  - 이름과 값의 쌍 => 프로퍼티
  - 이름과 값을 콜론(:)으로 구분
  - {}안에 여러 프로퍼티들이 있다면 서로 쉼표(,)로 구분
  - 프로퍼티 이름으로 모든 문자열과 식별자 사용 가능( "이름" : "값" 가능함)
  - 없는 프로퍼티 읽기 시도 -> undefined반환
  - 객체 리터럴{}안에 아무것도 작성하지 않으면 빈 객체 생성
 프로퍼티의 추가와 삭제
  - 없는 프로퍼티 이름에 값을 대입하면 새로운 프로퍼티가 추가됨
    var card = { suit: "하트", rank: "A"};
    card.value = 14;
    console.log(card);  //{suit: "하트", rank: "A", value: 14}
  - delete 연산자로 삭제
    delete card.rank;
  - in 연산자로 프로퍼티 확인
    "프로퍼티 이름" in "객체명"
    console.log("suit" in card);
      존재하면 true, 아니면 false
  - 사용 예시: 좌표평면의 점, 원의 중심과 반지름, 회원정보
  - 저장된 값이 함수인 프로퍼티 -> 메서드
 함수
  - function 키워드로 정의
    function square(x) { return x*x };
  - 함수 선언문을 프로그램의 첫머리로 '끌어올림'
  - 함수 선언하면 함수이름=변수이름 인 변수와 함수 객체 생성, 변수에 함수 객체의 참조가 저장됨. 변수값을 다른 변수에 할당하면 그 변수 이름으로 함수 실행 가능. 함수를 다른 함수의 인수로 넘기기 가능.
  - 원시 값을 인수로 넘겼을 때: 값 자체가 인자에 전달(값의 전달)
  - 객체를 인수로 넘겼을 때: 변수에 저장된 참조 값을 인자에 대입(참조 전달)
 변수
  - 전역 변수: 함수 밖에서 선언된 변수. 유효범위 = 프로그램 전체
  - 지역 변수: 함수 내부에서 선언된 변수. 유효범위 = 선언된 함수 내부
  - 전역 변수와 지역 변수의 이름이 같을 때: 함수 내부에서는 지역 변수를 채택
  - 함수 내부의 변수 선언은 끌어올려짐
  - let 선언자
    : 블록 유효 범위를 갖는 지역변수 선언
    let a, b, c;  (a, b, c의 유효 범위는 블록 내부)
    let으로 선언한 변수는 끌어올리지 않음
  - const 선언자
    : 블록 유효 범위를 가지면서 '한 번만 할당'가능한 지역변수 선언
 생성자 
  - new 연산자로 객체 생성
    function Card(suit, rank)
    {
      this.suit = suit;
      this.rank = rank;
    }
    var card = new Card("하트", "A");
    //suit 프로퍼티에 "하트", rank 프로퍼티에 "A"라는 값이 저장된 객체가 생성되고, 그 객체의 참조가 변수 card에 할당된다.
  - 생성자 안에서 this.프로퍼티 이름 에 값을 대입하면 그 이름을 가진 프로퍼티에 값이 할당된 객체가 생성됨 (this: 생성자가 생성하는 객체를 가리킴)
    var Card{};
    card.suit = "하트";
    card.rank = "A";
  - 생성자와 new 연산자로 생성한 객체: 그 생성자의 인스턴스
  - 이름은 같지만 프로퍼티 값이 다른 객체 여러개 생성 가능
    var card1 = new Card("하트", "A");
    var card2 = new Card("클럽", "K");
    var card3 = new Card("스페이드", "2");
    Card 생성자 안에 3개의 인스턴스(객체) 생성
  - this.프로퍼티 이름 에 함수의 참조를 대입해 메서드 정의
    function Circle(center, radius)
    {
      this.center = center;
      this.radius = radius;
      this.area = function() {return Math.PI * this.radius * this.radius;};
    }
    var p = {x:0, y:0};
    var c = new Circle(p, 2.0);
    console.log("넓이 = " + c.area());
  - Date 생성자: 날짜와 시간을 표현하는 객체 생성
    var now = new Date();
    console.log(now);   //Date객체의 날짜와 시간 정보
   - now.getFullYear()
     now.getMonth()
     now.getDate()
     now.getHours()
     now.getMinutes()
     now.getSeconds()
     now.getMilliseconds()
     now.toString()   //요일 월 일 년도 시간 지역시간
     now.toLocalString() //지역화된 시간과 날짜
     now.toLocalDateString()   //지역화된 날짜 정보
     now.toLocalTimeString()   //지역화된 시간 정보
     now.getUTCHours()   //UTC시각(협정 세계 시)
     now.toUTCString()   //UTC시간과 날짜 정보
  - Function 생성자: 함수 생성
    var 변수 이름 = new Function(인수1, 인수2, ... , 인수n, 함수 몸통);
      var square = new Function("x", "return x*x");
 배열
 ㅗㅓ호ㅗ료파ㅣ
 
