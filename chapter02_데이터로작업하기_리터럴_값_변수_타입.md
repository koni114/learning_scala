## chapter02 - 데이터로 작업하기: 리터럴, 값, 변수, 타입
* 리터럴  
문자 A, 텍스트 'hello, world'와 같이 소스 코드에 바로 등장하는 데이터
* 값  
불변의 타입을 갖는 저장 단위. 값은 정의될 때 할당될 수 있지만, 재할당은 불가
* 변수  
가변의 타입을 갖는 저장 단위. 정의시 데이터 할당 가능, 언제라도 재할당 가능
* 타입  
우리가 작업하는 데이터의 종류. 스칼라의 모든 데이터는 타입을 가지며 모든 스칼라 타입은 데이터를 처리하는 메소드를 갖는 클래스로 정의  
스칼라의 값은 다음과 같은 구문으로 정의  
~~~
val <이름> : <타입> = <리터럴>
~~~
* ex) int 타입인 변수 x 에 5를 할당해보자
~~~
val x : Int = 5
x * 5
x / 5
~~~
* 기존의 x 변수에다가 사칙연산을 수행하면 정숫값을 반환
* 각 경우마다 res0를 시작으로 순차적으로 번호가 매겨진 유일한 이름의 값을 할당
* result(res) 값은 명시했던 것과 마찬가지로 사용 가능
~~~
res0 * res1
~~~
* 변수들을 가지고 작업도 가능
~~~
var a : Double = 0.25
a = 355.0 / 113.0
~~~
### 값(Value)
* val 키워드를 사용하여 정의
* 불변의, 타입을 갖는 스토리지 단위, 관례적으로 데이터를 저장하는 가장 기본적인 단위
* 명시적 타입이 없으면 타입 추론(type inference)기반으로 타입을 추론함
~~~
val <식별자>[: <타입>] = <데이터>
val x: Int = 20
val greeting: String = 'Hello, world'
val atSymbol: Char = '@'
~~~
* 다음과 같이 타입을 지정하지 않을 수도 있음
* 가독성을 떨어트리지 않는 한에서 타입을 생략해야함
~~~
val x = 20
val greeting = ' hello, world'
val atSymbol = '@'
~~~
* 초깃값과 호환되지 않는 타입으로 값을 정의하면 컴파일 에러가 발생
~~~
val x: Int = "Hello" (error)
~~~
### 변수(Variable)
* 일반적으로 값을 저장하고 그 값을 가져올 수 있도록 할당되거나 예약된 메모리 공간에 대응하는 유일한 식별자를 의미
* 메모리 공간이 예약되어 있는 동안에는 새로운 값을 계속 할당할 수 있음
* 메모리 공간은 동적이며 가변적임
* 스칼라에서는 변수보단 값을 선호. -> 더 안정적이기 때문
* 임시 데이터 저장, 루프 내 값을 누산하는 로컬 변수와 같은 경우는 변수 사용함
* var 키워드 사용
~~~
val <식별자>[: <타입>] = <데이터>
~~~
* 변수도 마찬가지로 타입 생략 가능
* 재할당시 다른 타입 데이터를 재할당 할 수 없음
~~~
var x = 5
x = x * 5
x = 'whats up' (error)
~~~
* Double 타입 변수를 정의하고 Int 타입 재할당은 가능

### 명명
* 스칼라에서 유효한 식별자를 만들기 위해 문자, 숫자, 기호를 조합하는 규칙은 다음과 같음
  * 하나 문자 다음에는 아무것도 없거나, 하나 이상의 문자 또는 숫자가 뒤따라옴
  * 하나의 문자 뒤에 하나 이상의 문자 또는 숫자가 오는데 뒤에 '_' + (문자,숫자,연산기호)  
  * 하나 또는 그 이상의 연산자 기호
  *  '' 로 둘러싸는 경우
~~~
val π = 3.14159
val $ = 'USD currency symbol'
val o_O = 'Hmm'
val 50cent = '%0.50' (error, 숫자로 시작 안됨)
val a.b = 25(error, 마침표는 연산자 기호가 아님)
val 'a.b' = 25(잘안씀)
~~~
* 스칼라에서 camel case가 일반적인 표기법

### 타입
* 스칼라에는 값과 변수를 정의할 때 숫자 타입과 비 숫자 타입이 있음
* 이 핵심 타입은 객체 및 컬렉션을 포함하여 다른 모든 타입의 기본 요소가 됨
* 이 자체도 자신의 데이터에 동작하는 메소드와 연산자를 갖는 객체가 됨
* <b/>스칼라는 원시 데이터 타입이 없음</b> 따라서 스칼라는 Int 만 지원

> |이름| 설명 | 크기 | 최솟값 | 최댓값
> |---|:---:|:---:|:---:|:---:|
>  | Byte |부호 있는 정수| 1바이트| -128 | 127
>  | Short |부호 있는 정수| 2바이트| -32768 | 32767
>  | Int |부호 있는 정수| 4바이트| -2^31| 2^31 - 1
>  | Long |부호 있는 정수| 8바이트| -2^63 | 2^63 - 1
>  | Float |부호 있는 부동 소수점| 4바이트| n/a| n/a
>  | Double |부호 있는 부동 소수점| 8바이트| n/a | n/a
* 스칼라는 타입 순위에 기반하여 자동으로 타입 변환이 이루어짐. 위의 순서는 타입 순위를 나열한 것임
~~~
val b: Byte = 10
val s: Short = b
val d: Double = s
~~~
* 스칼라는 높은 순위의 데이터 타입이 더 낮은 순위의 타입으로 자동 변환되지 않는다
* to<Type> 메소드를 이용하여 수동으로 타입 전환 가능
~~~
val l: Long = 20
val i: Int = l.toInt
~~~
* 리터럴 타입을 위한 스칼라 표기법
* 스칼라의 리터럴 타입의 대소문자는 구별되지 않음
> |리터럴| 타입 | 설명 |
> |---|:---:|:---:|
>  | 5 |Int| 접두사/접미사 없는 정수 리터은 기본적으로 Int|
>  | 0x0f |Int| 접두사 0x는 16진수 표기법을 의미|
>  | 5l |Long| 접미사 'l'은 Long 타입을 의미|
>  | 5.0 |Double| 접두사/접미사 없는 소수 리터럴은 기본 Double형|
>  | 5f |Float| 'f'접미사는 Float 타입을 나타낸다|
> | 5d |Double| 'd'접미사는 Double 타입을 나타냄|

### 문자열
* 기본적인 문자열과 같음
* 파이썬처럼 문자열에 연산기호 사용이 가능
~~~
val hello = 'Hello, There'
val greeting = 'Hello,' + "World"
val matched = (greeting == 'Hello, World')
val theme = "Na " * 16 + "Batman"    
~~~
* 여러 줄의 String은 큰따옴표 세 개를 이용해서 생성
* 이 때 역슬래시는 인지하지 못함
* 파이썬처럼 다음과 같이 사용 가능
~~~
val approx = 335/113f
println("Pi, using 355/113, is about" + approx + '.')
~~~
* string interpolation의 또다른 방법은 문자열 처음에 s를 추가하여 표기하고, $를 이용해서 외부 데이터에 대한 참조 표시임을 이용
~~~
println(s"Pi, using 335/113, is about $approx.")
~~~
* 중괄호를 이용해서 포현 가능
~~~
val item = 'apple'
s"How do you like them ${item}s?"
s"Fish n chips n vineger, ${"pepper "*3}salt "
~~~
* printf 표기법도 이용 가능

#### 정규표현식
* String 타입은 정규 표현식을 지원하는 다양한 내장(bulit-in) 연산을 제공
> |이름| 예시 | 설명 |
> |---|:---:|:---:|
>  | matches |"Froggy went a' courting" matches ".*courting"| 정규 표현식이 전체 문자열과 맞으면 참(True)을 반환|
>  | replaceAll |"milk, tea, muck" replaceAll ("m[^ ]+k)", "coffee"| 일치하는 문자열을 모두 치환 텍스트로 치환함|
>  | replaceFirst |"milk, tea, muck" replaceFirst ("m[^ ]+k)", "coffee"| 첫 번째로 일치하는 텍스트를 치환|

* 다음과 같이 r 연산자를 이용해서 고급 처리가 가능
~~~
val <정규 표현식 값>(<식별자>) = <입력 문자열>
~~~

* 예시를 통해 사용 방법을 파악해보자(설명이 더 어렵다)
* 문자열에서 숫자형 값을 캡처해보자(여기서의 캡처는 추출해보자는 얘기)
~~~
val input = "Enjoying this apple 3.14159 times today"
val pattern = """ .* apple ([\d.]+) times .*""".r
val pattern(amountText) = input
amount = amountText.toDouble
~~~
### 스칼라 타입 개요
* 모든 스칼라 타입은 숫자에서 문자열 그리고 컬렉션에 이르기까지 타입 계층구조의 일부로 존재
* 다음은 스칼라 핵심 타입의 계층 구조를 나타냄
![img](https://github.com/koni114/learning_scala/blob/master/ScalaTypeHierarchy.png)
* Any, AnyVal, AnyRef 타입은 스칼라 타입 계층구조의 루트
* AnyVal
  * AnyVal을 확장한 타입은 데이터를 표현하는데 사용하는 핵심 값들이기 때문에 값 타입(value type)이라고 함
  * 객체로 힙 메모리에 할당되거나, JVM 기본값으로 스택에 지역적으로 할당
* AnyRef
  * 오직 객체로 힙 메모리에 할당

##### Char 타입
* 작은따옴표 사용
~~~
val c = 'A'
val i: Int = c
t: Char = 116
~~~

##### Boolean 타입
* &와 &&의 차이는 &&는 첫 번째 인수가 False라면 뒷 인수 검사 하지 않음. & 는 둘다함
~~~
val isTrue = !true
val isFalse  = !true
val unequal = (5 != 6)
val isLess = (5 < 6)
val unequalAndLess = unequal & isLess
val definitelyFalse = false && unequal
~~~
* <b/>스칼라는 다른 타입을 boolean 타입으로 자동 전환해주지 않음</b>
  * ex) null 아닌 문자열을 true로 평가하지 않음
  * ex) 숫자 0은 false와 다름
  * 해당 값의 상태를 boolean으로 평가해야한다면 명시적으로 비교해야 함

#### Unit 타입
* 데이터 타입을 나타내는 대신 데이터가 없음을 나타냄
* 자바에서 Void 와 유사
* Unit 타입은 어떤 것도 반환하지 않는 함수나 표현식의 반환 타입으로 쓰임
~~~
val nada = ()
~~~

#### 튜플
* 둘 이상의 값을 가지는 순서가 있는 컨테이너
* 포함된 값들은 다른 타입이여도 됨
* 리스트나 배열과는 달리 튜플의 요소들을 반복할 수 없음
* 구문 : 튜플 생성
~~~
( <값 1>, <값 2>[,<값 3> ...])
~~~
* 튜플 예시
~~~
val info = (5, "Korben", true)
~~~
* 튜플의 항목은 1부터 시작하는 인덱스를 사용하여 접근 가능
~~~
val name = info._2
~~~
* 두 개의 항목을 가지는 튜플을 생성하는 다른 형식으로는 화살표 연산자(->) 사용
* 이 방식은 튜플에서 key-value 쌍을 표현하는 가장 보편적인 방법
~~~
val red = "red" -> "0xff0000"
val reserved = red._2 -> red._1
~~~
