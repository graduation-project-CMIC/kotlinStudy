## Kotlin - Inheritance
<hr>

## Classes and Inheritance
* 상속
+ 코틀린의 최상위 클래스는 Any임
+ 클래스에 상위타입을 선언하지 않으면 Any가 상속됨

```
class Example1 //암시적인 Any 상속
class Example2 : Any() //명시적인 Any 상속
```

+ Any는 java.lang.Object와는 다른 클래스임
- Any에는 equals(), hashCode(), toString()만 있음

+ 상속해줄 클래스에서 open해주어야 된다.
```
class AA

class BB : AA()
//ERROR
```

```
open class AA

class BB : AA()
```

+ 파생클래스에 기본생성자가 없으면 각각의 보조생성자에서 상위타입을 super키워드를 이용해서 초기화 해주어야 함
+ 혹은 다른 생성자에게 상위타입을 초기화할 수 있게 위임해주어야 함.

```
class MyView : View{
    constructor() : super(1)//매개변수 없을 때, view에 있는 기본 생성자 불러서 super키워드를 이용해 초기화

    constructor(ctx : int) : this()//this()는 constructor()를 부름
    
    constructor(ctx : int, attrs : int) : super(ctx, attrs)
}
```
+ open annotation은 java의 final과 반대다.
+ open class는 다른 클래스가 상속할 수 있게 해줌
+ 기본적으로 코틀린은 모든 class는 final이다.

## Method Overriding

* 메소드 오버라이딩
+ 오버라이딩 될 메소드
- open annotation이 요구됨

+ 오버라이딩 된 메소드
- override annotation이 요구됨

```
open class Base{
    open fun v(){}
    fun nv(){}
}//오버리이딩 될 메소드

class Derived() : Base(){
    override fun v(){}
}//오버리이딩 된 메소드

```

### overriding rule
- 같은 멤버에 대한 중복된 구현을 상속받은 경우, 상속받은 클래스는 해당 멤버를 오버라이딩하고 자체 구현을 제공해야 함
- super + <클래스명>을 통해서 상위 클래스를 호출 할 수 있음

```
open class A{
    open fun f(){print("A")}
    fun a() {print("a")}
}
```

```
interface B{
    fun f(){print("B")}
    fun b(){print("b")}
}
```

```
class C() : A(), B{
    override fun f(){
        println("1")
        super<A>.f()
        println("2")
        super<B>.f()
        println("3")
    }
}
//result :  1
//          A
//          2
//          B
//          3
```

### abstract class

- abstract 멤버는 구현이 없음(body 필요 없음)
- abstract 클래스나 멤버는 open이 필요 없음

```
abstract class AbsClass{
    abstract fun f()
}

class MyClass() : AbsClass(){
    override fun f(){/* 구현 */}//상속받아서 직접 body 작성
}

```
