## chapter08 - 클래스
* 이제 클래스를 이용해 자신만의 타입을 만들어 보자
* 클래스(class)는 데이터 구조와 함수(메소드)의 조합으로, 객체지향 언어의 핵심 구성 요소
* 값과 변수로 구성된 클래스는 필요한 만큼 여러번 인스턴스화 될 수 있으며, 각 인스턴스는 자신만의 입력 데이터로 초기화될 수 있음
* 클래스는 상속(inheritance) 으로 다른 클래스로 확장할 수 있어 서브클래스와 슈퍼클래스의 계층구조를 생성할 수 있음
* 다형성(polymorphism)은 서브클래스가 부모 클래스를 대신하여 작업하는 것이 가능하게 함
* 캡술화는 클래스의 외관을 관리하는 프라이버시 제어를 제공

##### 가장 간단한 클래스 구문 만들기
~~~
class User
val u = new User
val isAnyRef = u.isInstanceOf[AnyRef]
~~~
* 값 u를 출력해보면, 클래스 이름과 16진수 문자열을 보게 되는데, 이는 해당 인스턴스에 대한 JVM reference
* 새로운 인스턴스를 생성하면 첫 번째 인스턴스와 메모리 위치가 다르고 따라서 다른 참조를 가지게 됨
* User 클래스 이름 뒤에 출력된 16진수 숫자를 출력하는 메소드는 JVM의 java.lang.Object.toString임
* java.lang.Object 클래스는 스칼라를 포함하여 JVM 내의 모든 인스턴스 루트이며, 기본적으로 스칼라 루트 타입인 Any와 동등
* 인스턴스를 출력함으로써 인스턴스가 루트 타입으로부터 상속한 toString 메소드를 호출
* User 클래스의 실제 부모 타입은 AnyRef

##### User class를 재설계하여 좀 더 유용하게 만들어보기
* 값과 그 값에서 동작하는 메소드 추가
* toString 메소드를 재정의하여 유용한 정보를 제공하는 버전을 제공
~~~
class User {
  val name: String = "Yubaba"
  def greet: String = s"Hello from $name"
  override def toString = s"User($name)"
}

val u = new User
println(u)
println(u.greet)
~~~
* 여기서 추가적으로 name을 매개변수로 값을 받아보자
~~~
class User(n:String) {
  val name: String = n
  def greet: String = s"Hello from $name"
  override def toString = s"User($name)"
}

val u = new User("Zeniba")
println(u)
println(u.greet)
~~~
* 클래스 매개변수 n은 클래스가 생성되고 나면 그 매개변수를 호출 불가(ex) u.n )

##### name 필드를 클래스 매개변수로 옮겨서 확인해보기
* 초기화를 위해 클래스 매개변수를 사용하는 대신 필드 중 하나를 클래스 매개변수로 선언할 수 있음
* 클래스 매개변수 앞에 val 또는 var 키워드를 추가하면 클래스 매개변수가 클래스의 필드가 됨
~~~
class User(val name: String) {
  def greet: String = s"Hello from $name"
  override def toString = s"User($name)"
}

val users = List(new User("Shoto"), new User("Art3mis")) // 클래스가 List의 타입 매개변수

val sizes = users map (_.name.size)
println(sizes)

val sorted = users sortBy (_.name)
println(sorted)

val third = users find (_.name contains "3")
print(third)

val greet = third map (_.greet) getOrElse "hi" //  
~~~
* 스칼라 개발자라면, 자신만의 클래스를 개발할 때, 컬렉션에서 그 클래스를 사용하게 됨

##### 상속과 다형성의 예제를 작성해보기
* 클래스는 extends 키워드를 이용하여 다른 클래스로 확장 가능
* override 키워드로 상속받은 메소드의 행위를 재정의 할 수 있음
* 클래스에서 필드와 메소드는 this 함수를 이용하여 접근 가능
* 클래스의 부모 클래스의 필드와 메소드는 super 키워드를 이용하여 접근 할 수 있음
~~~
class A {
  def hi = "Hello from A"
  override def toString = getClass.getName
}

class B extends A
class C extends B { override def hi = "hi C -> " + super.hi }

val hiA = new A().hi
val hiB = new B().hi
val hiC = new C().hi
~~~
##### 스칼라의 다형성 실습해보기
* 다형성은 클래스가 호환되는 다른 클래스의 모양새를 띄게 해주는 능력을 말함
* '호환된다'는 의미는 서브클래스의 인스턴스가 그 부모 클래스의 인스턴스를 대신해 사용될 수 있으나, 그 반대로는 가능하지 않음을 말함
~~~
val a: A = new A
val a: A = new B

val b: B = new A(error)
val b: B = new B
~~~
*
