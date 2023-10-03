원하는 이모지 넣기
 https://html-css-js.com/html/character-codes/icons/
 이 사이트에서 복붙하면 됨! 
 *주의해야 할 점
  이모티콘 별로 사용하는 비트가 달라서 이 점 유의해야 함
  문자열의 길이로 뭔가를 하는 함수를 처리할 때 문제가 생길 수 있음.
  문자열의 길이 확인

js에서는 utf-16사용
 - 16비트를 한글자로 표현함.
 - 16비트 코드 두개로 문자 하나를 표현 :surrogate pair

이모지가 surrogate pair로 표현되는지 확인하는 방법?
 - 유니코드 코드 포인트를 조사하기
 - Surrogate pair는 유니코드 코드 포인트를 16비트 단위로 나누어 표현하는 것이므로, 코드 포인트의 범위를 확인하여 surrogate pair를 식별할 수 있음

다음은 JavaScript에서 이모지가 surrogate pair로 표현되는지 확인하는 예제 코드입니다:
function isSurrogatePair(emoji) {
  // 이모지 문자열의 첫 번째 코드 포인트를 가져옵니다.
  const codePoint = emoji.codePointAt(0);

  // 유니코드 코드 포인트 범위를 확인합니다.
  // Surrogate pair는 0xD800에서 0xDFFF 사이의 코드 포인트를 사용합니다.
  return codePoint >= 0xD800 && codePoint <= 0xDFFF;
}

const emoji1 = '🧑‍🎓'; // surrogate pair를 포함하는 이모지
const emoji2 = '🍎';      // surrogate pair가 아닌 이모지

console.log(isSurrogatePair(emoji1)); // true
console.log(isSurrogatePair(emoji2)); // false

html에 대해서
1. 마크업 언어: HTML은 텍스트 기반의 마크업 언어로, 텍스트 문서 내에 태그와 속성을 사용하여 컨텐츠를 구조화하고 표현합니다.

2. 구조화: HTML은 웹 페이지의 구조를 정의하며, 제목, 단락, 목록, 링크, 이미지, 표, 폼 등과 같은 요소를 사용하여 페이지의 구성 요소를 나타냅니다.

3. 태그: HTML 요소는 여는 태그(`<tag>`)와 닫는 태그(`</tag>`)로 둘러싸인 형식을 가집니다. 예를 들어, `<h1>` 태그는 제목을 나타내며 `</h1>`로 닫습니다.

4. 속성: HTML 요소에는 속성(attribute)이 포함될 수 있으며, 속성은 요소에 대한 추가 정보를 제공합니다. 예를 들어, `<img>` 태그의 `src` 속성은 이미지 파일의 경로를 지정합니다.

5. 웹 브라우저와 렌더링: 웹 브라우저는 HTML 문서를 해석하고 렌더링하여 사용자에게 시각적으로 표시합니다. HTML은 웹 페이지의 구조와 내용을 정의하며, CSS(Cascading Style Sheets) 및 JavaScript와 함께 사용하여 디자인과 동작을 제어합니다.

6. 버전: HTML의 다양한 버전이 존재하며, 현재 주로 사용되는 버전은 HTML5입니다. HTML5는 다양한 멀티미디어 요소, 개선된 웹 폼, 지오로케이션 지원 등을 제공합니다.

7. 시맨틱 웹: HTML5는 시맨틱 태그(semantic tags)를 도입하여 웹 페이지의 의미와 구조를 더 명확하게 표현합니다. 예를 들어, `<header>`, `<nav>`, `<article>`, `<footer>`와 같은 시맨틱 태그를 사용하여 콘텐츠의 의미를 부여할 수 있습니다.

HTML은 웹 개발에서 기본적인 언어로 사용되며, 웹 페이지를 만들고 웹 애플리케이션을 구축하는 데 필수적입니다.
