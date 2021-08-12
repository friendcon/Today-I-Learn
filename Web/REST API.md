# 03. REST API

`**REST**`는 `**Representational State Transfer**`의 약자이다. 여러 리소스를 HTTP URI로 표현하고 리소스에 대한 행위를 HTTP Method로 정의하는 방식을 의미한다. 

REST API를 사용하게되면 그 자체만으로 `**API의 목적**`이 무엇인지 쉽게 알 수 있다. 

### REST API 관련 어노테이션

- `**RestController`** : 컨트롤러가 REST 방식을 처리하기 위한 것임을 명시한다.
- `**ResponseBody`** : 일반적인 JSP 같은 뷰로 전달되는게 아니라 데이터 자체를 전달하기 위한 용도이다.
- `**PathVariable`** : URL 경로에 있는 값을 파라미터로 추출하려고 할 때 사용한다.
- `**CrossOrigin`** : ajax 의 크로스 도메인 문제를 해결해주는 어노테이션.
- `**RequestBody**` : JSON 데이터를 원하는 타입으로 바인딩 처리를 한다

### @ RestController

순수한 데이터를 반환하는 형태이므로 다양한 포맷의 데이터를 전송할 수 있다. 일반문자열, JSON, XML 등 사용가능하다. 

기존 @ Controller 애너테이션의 경우 문자열을 반환하게되면 JSP 파일의 이름으로 처리를 하지만, @ RestController의 경우 순수한 데이터가 된다. 

@ GetMapping의 produces 속성은 메서드가 생산하는 MIME 타입이다. MIME이란 클라이언트에게 전송된 문서의 다양성을 알려주기 위한 것이다. 

### @ ResponseEntity

REST 방식으로 호출하는 경우는 화면 자체가 아니라 데이터 자체를 전송하는 방식으로 처리하기 때문에 요청한 쪽에서는 정상적인 데이터인지 비정상적인 데이터인지를 구분할 수 있도록 확실한 방법을 제공해야한다. 

데이터와 함께 HTTP 헤더의 상태 메세지 등을 같이 전달하는 용도로 사용한다. HTTP 상태 코드와 에러 메시지 등을 함께 데이터와 전송할 수 있기 때문에 받는 입장에서는 결과를 확실하게 알 수 있다. 

### RestController에서 파라미터

- `**@ PathVariable**` : 일반 컨트롤러에서도 사용이 가능하지만 REST 방식에서 자주 사용된다. URL 경로의 일부를 파라미터로 사용할 때 이용한다.

    REST 방식에서는 URL에 최대한 많은 정보를 담으려고 한다. 이전에는 ? 뒤에 추가되는 쿼리 스트링이라는 형태로 파라미터를 이용해서 전달되던 데이터들이 REST 방식에서는 경로의 일부로 차용되는 경우가 많다. 

- `**@ RequestBody**` : JSON 데이터를 원하는 타입의 객체로 변환해야 하는 경우 사용한다. 요청객체의 바디를 이용해서 해당 파라미터의 타입으로 변환을 요구한다. 대부분의 경우에는 JSON 데이터를 서버에 보내서 원하는 타입의 객체로 변환하는 용도로 사용되나, 원하는 포맷의 데이터를 보내고, 이를 해석해서 원하는 타입으로 사용하기도 한다.
- `**Consumes`** : 수신하고자 하는 데이터 포맷
- `**Produces`** : 출력하고자 하는 데이터 포맷

### 다양한 전송방식

 REST는 이전의 방식과는 다르게 GET/POST 이외에 다양한 방식으로 데이터를 전달할 수 있다. HTTP 의 전송 방식은 다음과 같다.

- Create : POST
- Read : GET
- Update : PUT
- Delete : DELETE

REST 방식은 URI와 결합하므로 회원이라는 자원을 대상으로 전송방식을 결합하면 다음과 같다.

- POST : /members/new
- GET : /members/{id}
- PUT : /members/{id} + body
- DELETE : /members/{id}