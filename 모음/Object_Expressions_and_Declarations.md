## Kotlin - Object Expressions and Declarations
<hr>

## Object
* object 용도
+ 어떤 class에서 조금 변경된 객체를 생성 할 때
+ 새로운 subclass의 명시적인 선언 없이 객체 생성

* Object Expressions
+ java 익명 객체를 대체할 수 있다
* Object Declarations
+ java 싱글턴처럼 사용
* Companion Object
+ 싱글턴 + class method(static을 대체해서 사용)
- kotlin에서는 static을 지원하지 않는다.

* 객체 표현식
- Java에서는 익명 내부 클래스르 사용해서 처리했음
- Kotlin에서는 object expressions을 이용
```
//java
btn.setOnClicklistener(new OnClickListener(){
    public void onClick(View v){

    }
});

//kotlin
window.addMouseListener(object : MouseAdapter(){
    override fun mouseClicked(e : MouseEvent){ }
    override fun mouseEntered(e : MouseEvent){ }
})

```

* 객체 표현식 상속
+ 슈퍼타입의 생성자가 있는 경우, 반드시 값을 전달 해 주어야함
+ 슈퍼타입이 여러 개인 경우 ':' 콜론 뒤에, ':'콤마로 구분해서 명시 해주면 됨

```
//기존 java에서의 표현
class  MyRunnable : Runnable {
    override fun run(){
        println("hello kotlin")
    }
}

fun main(args : Array<String>){
    val t = Thread(MyRunnable())
    t.run()
}
```

```
//kotlin에서의 object 개념 적용
fun main(args : Array<String>){
    val t = Thread(object : Runnable {
        override fun run(){
            println("hello kotlin")
        }
    })
    t.run()
}
```

* 객체 표현식 상속 없는 경우
+ 특별히 상속 받을 supertypes가 없는 경우, 간단하게 작성가능

```
val adHoc = object{
    var x : Int = 0
    var y : Int = 0
}

print(adHoc.x + adHoc.y)
```

* 객체 표현식 제약 사항
+ 익명 객체가 local이나 private으로 선언될 때만 type으로 사용될 수 있음
+ 익명 객체가 public function이나 public property에서 리턴 되는 경우, 익명객체의 슈퍼타입으로 동작됨, 이런 경우 익명 객체에 추가된 멤버에 접근이 불가능함

```
class C{
    private fun privatefoo()= object { val x : String = "x" }
    public fun publicFoo() = object { val x : String = "x" }

    fun bar() {
        val x1 = privatefoo().x //Works
        val x2 = publicFoo.x //Error
    }
}
```

* 객체 표현식 특징
+ 익명 객체의 코드는 enclosing scope의 변수를 접근할 수 있음
+ Java와는 다르게 final variables 제약 조건이 없음

* 객체 선언 용도
+ 매우 유용한 Singleton 패턴을 kotlin에서는 object declarations을 이용해서 만들 수 있음

```
object DataProviderManager{
    fun registerDataProvider(provider : DataProvider){
        // ...
    }

    val allDataProviders : Collection<DataProvider>
    get() = //...
}
```

* 객체 선언 문법
+ object 키워드 뒤에 항상 이름이 있어야함
+ object declaration은 object expression이 아님
+ 그래서 할당 구문의 우측에 사용될 수가 없음
```
object DataProviderManager{
    fun registerDataProvider(provider : DataProvider){}
    val allDataProviders : collection<DataProvider>
}
```

+ object declaration의 객체를 참조 하려면, 해당 이름으로 직접 접근하면 됨
```
DataProviderManager.registerDataProvider(...)
```

+ 슈퍼타입을 가질 수 있음(상속가능)
```
object DefaultListener : MouseAdapter(){
    override fun mouseClicked(e : MouseEvent){ }
    override fun mouseEntered(e : MouseEvenet){ }
}
```

## Companion Object

* 동반자 객체
+ 클래스 내부의 object declaration은 companion 키워드를 붙일 수 있음
```
class MyClass{
    companion object Factory{
        fun create():MyClass=MyClass()

    }
}
```
+ companion object의 멤버는 클래스 이름을 통해서 호출 할 수 있음
```
val instance = MyClass.create()
```

+ Companion object의 이름은 생략될 수 있음
+ 이런 경우 [class name].Companion 형태로 객체에 접근 가능
```
class MyClass{
    companion object{

    }
}

val x = MyClass.Companion
```

+ companion object의 멤버가 다른 언어의 static 멤버처럼 보일 수 있지만 아님
+ companion object의 멤버는 실제 객체의 멤버임
+ 슈퍼클래스도 가질 수 있는 클래스의 객체임

```
interface Factory<T>{
    fun create() : T
}

class MyClass{
    companion object : Factory<MyClass>{
        override fun create() : MyClass = MyClass()
    }
}
```

## Object expression vs Object declaration
- object expression는 즉시 초기화 되고 실행된다.
- object declarations는 나중에 초기화 된다. (최초 접근 시)
- companion object는 클래스가 로드될 때 초기화 됨, java static initializer와 매칭됨