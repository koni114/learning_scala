## chapter04 - 함수
* 함수형 프로그래밍 언어에서 함수는 굉장히 중요
* 함수형 프로그래머는 단일-목적으로 작성된 함수를 갖고 일련의 연산을 수행할 것임
* 순수 함수 를 따르면 더 훌륭한 이점을 얻을 수 있음
* 순수 함수의 특징
  * 하나 또는 그 이상의 입력 매개변수를 가짐
  * 입력 매개변수만을 가지고 계산 수행
  * 값을 반환
  * 동일 입력에 대해 항상 같은 값을 반환
  * 함수 외부의 어떤 데이터도 사용하거나 영향을 주지 않음
  * 함수 외부 데이터에 영향을 받지 않음
* 스칼라 애플리케이션을 모듈화하고 조직화 하는 일반적인 목표는 순수하지 않는 함수를 분명하게 명명하고 순수함수와 쉽게 구분해 낼 수 있는 방식으로 구성하는 것

#### 함수의 가장 기본적인 형태
~~~
def <식별자> = <표현식>
~~~
* 현행 데이터의 포멧을 만들 때
* 새로운 데이터를 위한 원격 서비스를 확인할 때
* 단지 고정값을 반환하는 함수가 필요할 때
~~~
def hi = "hi"
~~~
#### 구문: 반환 타입을 지정하여 함수 정의하기
* 함수의 반환 타입은 값이나 변수의 타입과 마찬가지로, 정의되지 않더라도 존재한다
* 함수도 명시적 타입을 지정해야 더 읽기 쉬움
~~~
def hi: String = "hi"
def multiplier(x:Int, y:Int): Int = {x * y}
~~~
* 마지막 줄은 함수의 반환 값
* 만약 중간에 종료하려면 return 사용
* 보편적으로 함수의 조기 종료는 입력값이 유효하지 않거나, 비정상적인 경우에 사용
~~~
def safeTrim(s: String): String = {
	if (s == null) return null
	s.trim()
}
~~~
### 프로시저(procedure)
* 프로시저는 반환값을 가지지 않는 함수
* println과 같이 statement를 사용하는 함수도 프로시저
* 마지막에 타입을 Unit으로 명시하면 코드를 읽는 사용자에게 반환값이 없다는 것을 분명하게 나타냄
~~~
def log(d: Double) = println(f"Got value $d%.2f")
def log(d: Double): Unit = println(f"Got value $d%.2f")
~~~

### 빈 괄호를 가지는 함수
* 괄호가 없는 것보다 있는 것이 더 좋은 함수 표기법
~~~
def hi(): String = "hi"
~~~
* 빈괄호를 써서 함수를 정의 하고 호출하는경우, 괄호가 있던 없던 호출 가능
* 빈괄호를 안쓰고 함수를 정의하는 경우, 괄호를 쓰면 error 발생

### 표현식 블록을 이용한 함수 호출
* 함수에 계산된 결과 값을 바로 전달하는 경우 사용
~~~
def formatEuro(amt: Double) = "f"$amt%.2f""
formatEuro(3.4645)
formatEuro {val rate =  1.32; 0.235 + 0.7123 + rate * 5.32}
~~~  

### 재귀 함수
* 기본 예제
~~~
def power(x:Int, n:Int): Long = {
	if (n >= 1) power(x, n-1)
	else 1
}
~~~
* stack overflow 에러에 빠지지 않도록 조심해야함
* 재귀적 호출이 추가적인 스택 공간을 사용하지 않도록 꼬리 재귀(tail-recursion)을 사용하자  
마지막 문장이 재귀적 호출인 함수만이 꼬리-재귀를 최적화 시킬 수 있음
* tail-recursion 위해 최적화될 함수를 표시하는 function annotation이 존재함  
함수가 꼬리 재귀로 최적화 될 수 없으면 error 발생  : @annotaion.tailrec 추가

* error가 발생하는 경우: 마지막 호출이 재귀 함수가 아님
~~~
@annotation.tailrec
def power(x:Int, n:Int): Long = {
	if (n >= 1) x * power(x, n-1)
	else 1
}
~~~
* error가 발생하는 경우2 : 마지막 호출이 재귀가 아니라 곱셈
~~~
@annotation.tailrec
def power(x:Int, n:Int): Long = {
	if (n <= 1) 1
	else x * power(x, n-1)
}
~~~
* 정상적으로 작동하는 경우
~~~
@annotation.tailrec
def power(x:Int, n:Int, value:Int): Long = {
if(n <= 1) value
else power(x, n-1, x*value)
}
~~~
* 꼬리 재귀는 가변 데이터를 사용하지 않고 반복할 수 있는 유용한 방법

### 중첩 함수
* 메소드 내에 반복해서 사용해야 할 필요가 있는 로직이 있는데,  
외부 메소드로써는 사용되지 않는 경우 중첩 함수로 사용
~~~
def max(a: Int, b: Int, c: Int): Int = {
	def max(a: Int, b:Int): Int = {if (x > y) x else y }
	max(a, max(b, c))
}
~~~
* 이 때 외부 함수와 내부 함수의 매개변수가 다르므로, 충돌은 없음
* 스칼라 함수는 함수 이름과 매개 변수 타입 목록으로 구분됨
* 위 같은 경우에 매개변수가 같다고 할지라도 내부함수가 우선되기 때문에 결과적으로 충돌나지 않음

### 이름으로 매개변수를 지정하여 함수 호출하기
* 스칼라 함수는 매개변수의 이름으로 호출이 가능하므로, 꼭 순서를 맞추지 않아도 됨
* 매개변수의 이름으로 함수를 호출하는 경우
~~~
def greet(prefix: String, name: String) = s"$prefix $name"
greet(prefix = 'Mr', name = "Brown")
~~~

### 기본을 갖는 매개변수
* 스칼라는 모든 매개변수에 기본값을 지정하도록 하고,  
호출자가 해당 매개변수를 선택적으로 사용하도록 함
~~~
def greet(prefix: String = "", name: String) = s"$prefix$name"
val greeting1 = greet(name = "Paul")
~~~
* 필수 매개변수가 먼저 오도록 배치하면, 이름을  호출하지 않고도 사용 가능

### 가변 매개변수
* 가변 인수(vararg)는 0개 이상의 여러 인수가 일치할 수 있는 함수 매개변수
* 스칼라도 가변 매개변수를 지원함으로써 정해지지 않는 개수의 입력 인수들로 함수를 정의할 수 있도록 함
* 가변 매개변수는 반드시 불변 매개변수 뒤에 위치해야 함
* 함수 정의에서 * 를 추가하면 해당 매개변수를 하나 이상의 입력 인수와 일치시키는 것
~~~
def sum(items: Int*): Int = {
	var total = 0
	for (i <- items) total += i
	total
}
~~~
### 매개변수 그룹
* 지금까지는 매개변수 리스트를 하나의 괄호를 묶어서 함수를 생성했는데,  
여러개의 괄호를 사용해 여러 그룹의 매개변수로 나누는 방식을 제공함
~~~
def max(x: Int)(y: Int) = if (x > y) x else y
max(10)(20)
~~~

### 타입 매개변수
* 스칼라에서는 값 매개변수를 보완하기 위해 값 매개변수 OR 반환값에 사용될  
타입을 지시하는 타입 매개변수를 전달할 수 있음
* 타입 매개변수로 함수를 정의하는 구문은 다음과 같음
~~~
def <함수명>[타입명](<매개변수 이름>: <타입명>): <타입명> ...
~~~
##### 타입 매개변수 예시
* 입력 값을 그대로 반환하는 항등 함수(identity function)를 만들어보자
~~~
def identify(s: String): String = s
~~~
* 위의 식으로는 String만 호출이 가능하다. 다른 함수를 정의하지 않는 한 다른 타입(ex) Int) 를 호출할 수 없음
* 그렇다면 Any type을 만드는 것은 어떨까?
* 다음 생성된 예제를 보자
~~~
def identity(a: Any): Any = a
val s: String = identity("Hello")  (error)
~~~
* 결과적으로 error를 발생시킴.   
그 이유는 함수의 반환값이 Any type 이기 때문에 String type에 담지 못함
* 이 때 타입 매개변수를 사용하면 어떤 타입이던지 반환값으로 만들어 사용할 수 있음!
~~~
def identity[A](a: A): A = a
val s = identity[String]("Hello")
val d = Double = identity[Double](2.717)
~~~
* 스칼라의 특징 중 하나는 타입 추론인 만큼,  
타입 매개변수에 타입을 넣지 않아도 추론하여 전환됨
~~~
val a: String = identity("hello")
val d: Double = identity(0.333)
~~~
* 값 변수의 타입 자체도 추론할 수 있으므로, 생략해도 됨
~~~
val a = identity("Hello")
val b = indentity(0.333)
~~~
* 이 예제는 스칼라 타입 시스템의 유연성과 기능성, 재사용성이 높은 함수를 보여줌

### 메소드와 연산자
* 함수는 객체(object) 안에 존재하며, 객체의 데이터에 동작하므로 이러한 함수를 칭하는 더 적절한 용어는 <b/>메소드(method)</b>임
* <b/>메소드는 클래스 내에서 정의한 함수</b>
* 메소드를 호출하는 방식은 자바에서와 동일(.를 이용)
* String 타입에 적용하는 많은 유용한 메소드 중 하나를 호출해보자
~~~
val s = "vacation.jpg"
val isJPEG = s.endsWith(".jpg")
~~~
* Double 타입에 유용한 메소드 몇 가지를 사용해보자
~~~
val d = 65.642
d.round
d.floor
d.compare(18.0) // d 가 매개변수보다 크면 1, 같으면 0, 작으면 -1 반환
d.+(2.721)
~~~
* 우리가 사용하는 모든 연산자는 실제로 메소드임. 함수 이름처럼 연산자 기호를 사용하여 쓰임
* 이는 <b/>연산자 표기법(operation notation)</b>으로 알려진 객체의 메소드를 호출하는 다른 형태,
점 기호를 버리고 공백을 사용하는(ex) a + b) 방식 덕분에 가능
* 이러한 표기법을 정확히 infix operator notation이라고 함
* 마지막 두 메소드 호출을 연산자 표기법을 사용하여 다시 작성해보자
~~~
d compare 18.0
d + 2.721
~~~
* 여러개의 매개변수가 있는 경우, 연산자 표기법을 사용하려면, list로 묶어 단일 연산자로 취급해야함

### 가독성 있는 함수 작성하기
* 함수를 어떻게 작성할 것인가?
* 함수를 쓰는 것은 이를 <b/>재사용</b> 한다는 것
* 함수를 읽기 쉽게 만들기
  * 함수가 하고자 하는 일을 합리적으로 요약할 수 있는 이름을 사용
  * 사용자가 전체 함수를 보기 위해 스크롤을 위아래로 움직이지 않아도 되게 하기
* 주석 추가하기
  * 한줄 주석 : //
  * 범위 주석 : /* */
  * scaladoc 해더 추가 : /** 시작하여 */로 종료
  * 매개변수는 @param 키워드 다음에 매개변수 이름과 설명을 붙이기
~~~
/**
  * 선행 혹은 후행 공백 없이 입력 문자열을 반환
  * 입력 문자열이 Null인 경우, null을 반환
  * 매개변수 s는 입력 문자열
  */
def safeTrim(s: String): String = {
  if(s == null) return null
  s.trim()
}
~~~

##### 용어 정리
* IDE : 통합개발환경(Integrated Development Environment)  
코딩, 디버그, 컴파일, 배포 등 프로그램 개발에 필요한 작업을  
하나의 프로그램에서 제공해주는 개발 환경을 의미
