# Erros와 ValidationUtils 클래스의 주요 메서드

### Erros 인터페이스

* reject(String errorCode)
* reject(String errorCode, String defaultMessage)
* reject(String errorCode, Object\[] errorArgs, String defaultMessage)
* rejectValue(String field, String errorCode)
* rejectValue(String field, String errorCode, String defaultMessage)
* rejectValue(String field, String errorCode, Object\[] errorArgs, String defaultghyMessage)

**에러 코드에 해당하는 메시지, 인덱스 기반 변수를 포함하는 경우**

* Object \[] 타입의 errorArgs 파라미터 이용
*   defaultMessage 파라미터 메서드 사용하면,

    에러 코드에 해당하는 메시지가 존재하지 않을 때 defaultMessage 출력

***

### ValidationUtils 클래스

* rejectIfEmpty(Errors errors, String field, String errorCode)
* rejectIfEmpty(Errors errors, String field, String errorCode, Object\[] errorArgs)
* rejectIfEmptyOrWhitespace(Errors errors, String field, String errorCode)
* rejectIfEmptyOrWhitespace(Errors errors, String field, String errorCode, Object\[] errorArgs)

<mark style="color:yellow;">rejectIfEmpty()</mark>

* field에 해당하는 프로퍼티 값이 null 혹은 빈문자열(””)이면 에러 코드로 errorCode 추가

<mark style="color:yellow;">rejectIfEmptyOrWhitespace()</mark>

* null, 빈 문자열, 공백 문자(스페이스, 탭)으로만 값 구성 경우 에러 코드 추가
* 에러 코드에 해당하는 메시지나 인덱스 기반 플레이스홀더 포함 시
  * errorArgs를 이용해서 삽입할 값 전달
