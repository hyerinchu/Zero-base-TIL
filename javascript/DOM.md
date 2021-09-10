# DOM이란 ? (Document Object Model)

document : html로 이해하기
object : 객체(javascript의 자료형중 하나)
Model : modeling 했다

- > html 을 object로 modeling 했다
- > .html 을 javascript도 이해할 수 있는 object(객체)로 만든것
- > DOM은 브라우저에 내장되어 있는 API
- > 브라우저는 CSS또한 CSSOM이란 API를 이용해 Javascript 가 이해할 수 있는 object(객체)로 만들어 준다

- 브라우저는 html문서를 해석하고 화면을 통해 해석된 결과를 보여준다
- 브라우저(ex 크롬, 사파리)가 HTML 코드를 해석해서 요소들을 트리 형태의 계층구조로 표현하는 문서(데이터)를 생성한다
- 이를 'DOM'이라고 한다

- 브라우저는 DOM 을 먼저 생성한 후
- DOM을 활용해 화면에 웹 콘텐츠들을 렌더링 한다

#

## DOM 의 목적

> html을 javascript가 이해할 수 있는 객체로 만들어서 웹 화면의 콘텐츠를 추가,수정,삭제 하거나 이벤트를 처리할 수 있도록 프로그래밍 인터페이스를 제공한다
