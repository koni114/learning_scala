## chapter03 표현식과 조건문
* 표현식과 문장, 조건문에 대해서 설명한다
* 함수와 표현식은 우리가 제공한 입력값에 대해서만 동작하고 반환값 이외에는 영향을 주지 않음  
이는 함수형 프로그래밍의 주요 목표이자 이점 중 하나
### 표현식
* 표현식(expression)은 값을 반환하는 코드의 단위
* 시작으로 간단한 스칼라 표현식을 예로 들어보자
~~~
"hello" (리터럴 값)
"hel" + "l" + "o" (계산된 값)
~~~
* 두 예제는 서로 다른 방식으로 구현되었지만 동일한 결과 값을 반환
* 표현식에서 중요한 것은 단지 <b/>반환하는 값</b> hello" (리터럴 값)

#### 표현식으로 값과 변수 정의하기
* 표현식이 리터럴, 계산식 또는 함수호출 어디든 해당하더라도 성립한다는 것을 기억하자
#####  표현식을 이용하여 값과 변수 정의하기
~~~
val <식별자>[:<타입>] = <표현식>
var <식별자>[:<타입>] = <표현식>
~~~
#### 표현식 블록
* 여러 표현식을 중괄호를 사용하여 하나로 묶어 단일 표현식 블록(expression block)을 만들 수 있음
* 표현식은 자신만의 범위를 가지고, 블록 내에 국한된 값과 변수를 포함함
* 마지막 표현식이 전체 블록의 반환값이 됨
~~~
val x = 5 * 20; val amount = x + 10(표현식 사용 안 한 경우)
val amount = {val x = 5 * 20; x + 10}(표현식 사용 한 경우)
~~~
* 표현식을 사용한 경우가 코드가 더 깔끔해졌다고 할 수 있는데, 그 이유는 x를 사용하는 의도가  
amount를 정의하기 위한 것임이 분명해졌기 때문  

* 표현식 블록은 여러 줄로 확장 가능
~~~
val amount = {
	val x = 5 * 20
	x + 10
}
~~~
* 표현식 블록 역시 중첩이 가능 - 제어구조를 사용할 때 중첩을  사용한다
~~~
{val a = 1; {val b = a * 2; {val c = b + 4; c}}}
~~~
#### 문장(statement)
* 값을 반환하지 않는 표현식
* 문장의 반환 타입은 Unit
* 보편적으로 사용되는 문장들에는 println() 호출과 값/변수 정의가 있음
~~~
val x = 1
println(1)
~~~
* 문장 블록은 기존 데이터를 수정하거나,   
애플리케이션 범위 밖(ex) 콘솔, DB 업데이트 등)을 변경하는데 사용  

### If .. Else 표현식 블록
* 스칼라는 if와 else블록만을 지원하며, else if 블록을 단일 구성체로 인식하지 않음
* 하지만 스칼라에서는 else if 가 정상적이게 동작하는데, 그 이유는 if .. else {if .. else}로 인식되기 때문

#### If 표현식
##### 구문: If 표현식 사용하기
~~~
if (<boolean 식>) <표현식>
~~~
~~~
if (47 % 3 > 0) println("Not a multiple of 3")
~~~
* if 블록 자체가 위처럼 문장(Statement)이 아닌 표현식으로 사용되면 문제가 있는데,  
if문이 False일 때 Any type으로 return된다
~~~
val result = {if(false) "what does this return?"}
~~~

#### If-Else 표현식
~~~
if (boolean식) <표현식> else <표현식>
~~~
* If-Else 예제
~~~
val x = 10; val y = 20
val max = if(x > y) x else y
~~~
* if 표현식에서는 반드시 중괄호를 사용해야 하며, if else는 한줄에 쓸 수 있다면 중괄호 없어도 됨

### 매치 표현식
* 스칼라에서는 조건부 로직을 작성하는 좀 더 좋은 방법으로 매치 표현식을 사용할 수 있음
* C의 Switch문과 유사
* 여러개의 case에 해당 될 때, 가장 먼저 걸리는 case에 본문을 읽고 종료  
-> 매치 표현식은 0개 또는 단 하나의 패턴만 매칭할 수 있어 break문을 사용하지 않음
* 스칼라의 매치 표현식은 타입, 정규 표현식, 숫자 범위, 데이터 구조 내용 같은 다양한 항목을 매칭할 수 있을 만큼 유연함
* 대부분의 스칼라 개발자는 매치 표현식을 if else문 보다 선호함
*
##### 구문:매치 표현식 사용하기
~~~
<표현식> match {
	case <패턴 매치> => <표현식>
	[case...]
}
~~~
* 만약 case 블록에 다중 표현식이 있다면, 이를 중괄호로 감싸서 표현식 블록으로 전환
* 위의 if .. else문을 match문으로 전환해보자
~~~
val x = 10; val y = 20
val max = x > y match {
	case true => x
	case false => y
}
~~~
* 표현식의 반환값 외에 추가적인 동작도 가능
* 다음 예시는 error를 반환하는 동시에 println도 함께 수행함
~~~
val message =  status match {
	case 200 =>
			"ok"
	case 400 => {
		println ("ERROR - we called the service incorrectly")
		"error"
	}
	case 500 => {
		println("ERROR - the service encountered an error")
		"error"
	}
}
~~~
* 마지막 표현식만 매치 표현식의 반환 값으로 사용
* '|' 를 이용하여 여러 패턴에 대한 동일 결과 값 리턴 가능
~~~
val kind = day match {
	case "MON" | "TUE" | "WED" | "THU" | "FRI" =>
	"weekday"
	case "SAT" | "SUN" =>
	"weekend"
}
~~~
* 해당 구문에서 "MONDAY"를 입력하면 런타임 에러 오류를 발생시킨다
* 에러를 안나게 하려면 wildcard match-all 패턴을 사용해야함

### 와일드카드로 매칭하기
* 와일드카드 패턴에는 값 바인딩(value binding)과 와일드카드 연산자가 있음
* 값 바인딩
  * 매치 표현식의 입력 패턴은 로컬 값에 바인딩되어 case 블록의 본문에서 사용가능

~~~
val message = "OK"
val status = message match {
	case "OK" => 200
	case other => {
		println(s"Couldn't parse $other")
	}
}
~~~

#### 와일드카드로 매칭하기
* 매치 표현식에서 사용할 수 있는 와일드카드 패턴에는 값 바인딩과 와일드카드 연산자가 있음
* 와일드카드를 사용하는 이유는, 단순 match에서 match되는 값이 없으면 error를 발생시키기 때문
##### 값 바인딩
* 값 바인딩을 사용하면 매치 표현식의 입력 값을 본문에 사용 가능
* 매칭되는 값이 없더라도 바인딩 된 값을 본문에 사용하므로, error를 발생하지 않고 예외처리가 가능
* 실제 값을 case 앞에 쓰는 경우가 아닌 변수를 쓰는 경우는 반드시 바인딩 되어 사용됨  
###### 구문: 값 바인딩 패턴
~~~
case <식별자> => <하나 이상의 표현식>
~~~

* 특정 리터럴과 매칭하고 그 외의 경우는 값 바인딩을 사용하여 가능한 다른 모든 값이 매치되도록 하기
~~~
val message = "OK"
val status = message match {
case "OK" => 200
case other => {
  println(s"Couldn't parse $other")
  -1
    }
}
~~~
* 값 other는 case 블록이 유지되는 동안 정의되며, 매치 표현식의 입력값인 message의 값이 할당됨  
(꼭 other라고 쓰지 않아도 상관없음)

##### 와일드카드 연산자
* 이 연산자는 '_'기호로 표시되며, 런타임에 표현식의 최종값이 들어갈 자리의 이름을 대신하여 자리표시자 역할을 함
* '_'기호는 매칭할 패턴을 제공하지 않기 때문에 어떤 입력값과도 매칭되는 와일드카드 패턴이 됨

###### 구문: 와일드카드 연산자 패턴
~~~
case _ => <하나 이상의 표현식>
~~~
*  _ 기호는 화살표 오른쪽에서 '_'  로 접근 불가능
* 와일드카드의 값에 접근하려면 값 바인딩을 쓰거나 매치 표현식의 입력값(message 자체) 에 접근을 고려해야함
~~~
val message = "Unauthorized"
val status = message match {
  case "OK" => 200
  case _ => {
    println(s"couldn't parse $message")
  }
}
~~~
* 즉 case _에서 달러_를 사용할 수 없고 $message를 사용해야 된다는 얘기!

##### 패턴 가드를 이용한 매칭
* case 다음에 오는 표현식에 if 구문이 올 수 있음
* 이 때 중괄호를 잘 사용하지 않는다
~~~
val response: String = null
response match {
  case s if s != null => println(s"Received '$s'")
  case s => println("Error ! Received a null response")
}
~~~

##### 패턴 변수를 이용한 타입 매칭
* 입력 표현식의 타입을 매칭하는 방법도 있음
* 매칭된다면 패턴 변수는 입력값을 다른 타입의 값으로 전환할 수 있음
* 패턴 변수(case 뒤에 오는 변수)는 반드시 소문자이어야 함*
* <b/>매치 표현식을 사용하여 값의 타입을 결정하는 방법 적용 가능</b>
  스칼라는 다형성을 가지므로, Int 타입의 값이 Any 타입의 다른 값에 할당되거나 자바나 스칼라 라이브러리 호출로부터 Any로 반환될 수도 있음
* 예제를 보면 더 잘 이해 될 것임
~~~
object practice {
  def main(args: Array[String]): Unit = {
    val x: Int = 12180
    val y: Any = x
    y match {
      case x: String => println(s"'x'")
      case x: Double => println(f"$x%.2f")
      case x: Float => println(f"$x%.2f")
      case x: Long => println(s"${x}l")
      case x: Int => println(s"${x}i")
    }
  }
}
~~~
* y의 값이 Any 타입을 가지더라도 Int로 생성되어 출력됨(i가 붙음)
* 즉  실제 가지고 있는 타입이 Any 더라도 실제 타입을 기반으로 매칭할 수 있음
* 따라서 정수 12180은 Any 타입이 주어졌어도 정수로 인식하고 그에 맞는 포맷을 갖게 됨

### 루프
* 스칼라에서 가장 중요한 루프는 for-루프로, for-comprehension이라고도 함
* 반복할 때마다 표현식을 실행하며, 선택적으로 반환값들을 컬렉션(collection)으로 돌려줌
* for 루프는 중첩, 필터링, 값 바인딩을 지원하는 등 customizing이 쉬움

* 스칼라에서는 Range 라고 불리우는 새로운 데이터 구조가 있음
* to, until 연산자를 이용해서 시작과 끝을 나타냄
* to : 끝을 나타내는 정수를 포함
* until : 끝을 나타내는 정수를 포함하지 않음

##### 구문: 숫자 범위 정의하기
~~~
<시작 정수값> [to|until] <끝 정수값> [by increment]
~~~

##### for 루프 정의하기
~~~
for (<식별자> <- <반복자>)[yield][<표현식>]
~~~
* 이 때 yield는 선택사항. yield가 쓰이면 컬렉션으로 반환
* for 루프 사용시 괄호나 중괄호를 이용해서 사용 가능. 두 표기법의 차이는 한 줄에 다중 for문을 사용하는지, for문 한개를 사용하는지의 차이임
* 괄호를 사용할때는 마지막 반복자 전에 ;를 붙여야 함
* 다음 예제들의 결과들을 보면서 감을 익히자
~~~
for (x <- 1 to 7){ println(s"Day $x:")}
~~~
~~~
val test = for (x <- 1 to 7) yield {s"Day $x:"}
println(test)
~~~
* IndexedSeq 의 서브타입인 Vector는 IndexedSeq 타입을 가지는 값에 할당 가능
* 이 컬렉션은 다른 for 루프에서 반복자로 사용가능
~~~
for (day <- test) print(day + ", ")
~~~

#### 반복자 가드
* 쉽게 말하면, for 루프 괄호 안에 if 표현식 사용 가능
~~~
val threes = for (i <- 1 to 20 if i % 3 == 0) yield i
~~~

* if문은 줄 구분을 통해서 여러개의 조건을 나타낼 수 있음
~~~
val quote = "Faith,Hope,,Charity"
for {
  t <- quote.split(",")
  if t != null
  if t.size > 0
}
{println(t)}
~~~

#### n중 for 문
* 우리가 일반적으로 생각하는 n중 for문은 다음과 같이 사용한다(비슷하다)
~~~
for {x <- 1 to  2
     y <- 1 to 3 }
    {print(s"($x, $y) ") }
~~~

#### 값 바인딩
* for 루프에서 값 바인딩이 가능
* 스칼라에서 보이는 독특한 방법. 표현식에서 크기가 복잡도를 줄여줌
* 바인딩된 값은 if문 내, 다른 바인딩된 값을 위해 사용 가능
~~~
val powersOf2 = for (i <- 0 to 8; pow = 1 << i) yield pow
~~~

#### While과 Do/While 루프
* for 루프 만큼 보편적이게 사용 안함
* yield 생성이 불가하며, 루프가 표현식이 아님
~~~
var x = 10; while (x > 0) x -= 1
~~~
~~~
val x = 0
do println(s"Here I am, x = $x") while (x > 0)
~~~
* 코드를 작성할 때 표현식 관점에서 작성하는 것은 굉장히 중요
* 표현식을 작성할 때 주의해야 할 중요한 원칙
  * 우리의 코드를 표현식으로 어떻게 구조화 할 것인지,
  * 어떻게 표현식이 반환값을 유도할 것인지,
  * 그 반환값으로 무엇을 할 것인지,
