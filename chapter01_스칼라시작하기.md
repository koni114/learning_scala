## chapter01 - 스칼라 시작하기
### 스칼라란?
*  스칼라(Scala)는 확장 가능한 언어(Scalable language)의 줄임말
* 자바 가상 머신(JVM) 플랫폼에서 함수형 프로그래밍과 객체지향 프로그래밍을 동시에 지원하는, 성능이 우수한 환경을 제공하기 위해 언어를 만듬

### 스칼라 설치하기
* 스칼라는 JVM 기반 언어로 자바 런타임(Java runtime)을 사용해야함
* oracle site에서 JDK를 설치하자
* command 창에서 다음의 명령줄을 통해 JDK가 제대로 설치되었는지 확인 가능
~~~
java -version
~~~
* 스칼라 설치하기
* 스칼라를 자동으로 설치하려면 OS X의 Homebrew, 원도우의 Chocolately, 리눅스에서는 apt-get/Yum과 같은 패키지 메니저를 사용하면 됨
~~~
(brew/choco/apt-get/yum) install scala
scala
~~~
* scala 명령어를 통해 제대로 설치가 되었는지 확인

### 스칼라 REPL 사용하기
* Read, Evaluate, Print, Loop의 앞글자를 딴 말. 쉽게말해서 cmd창에서 scala를 실행시키는 방식을 말함
* cmd 창에서 scala 명령어를 실행하면 REPL 셸 사용 가능
~~~
println("hello world")
~~~
* 화살표 위아래를 활용해서 이전/이후로 이동 가능
~~~
3 * 5
~~~
* 해당 수식을 prompt에 입력하면, res0: Int = 15 라는 결과를 출력함
* 이는 변수를 입력하지 않더라도 자동으로 res0 라는 변수를 생성해 값을 할당시킴
* res0를 이용해서 다른 연산을 수행해보자
~~~
res0 * 10
~~~
* 마찬가지로 해당 결과 값을 res1에 할당함
* 뒤에 붙은 숫자는 sequence처럼 붙여서 사용됨
* 스칼라는 정적 타입 시스템을 가진 컴파일 언어(한줄 실행이 가능)이기 때문에 바로바로 결과를 확인할 수 있음
