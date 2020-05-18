CMIC Kotlin에 대한 스터디 기록 파일입니다
=======================================

**Commit convention rule** : 날짜-[주제]-내용-상태

## 📌 Basic Syntax

#### 1. 함수정의

1. return
함수는 fun 키워드로 정의한다.

```
fun sum(a: Int, b: Int):Int{
    return a+b
}
```

paramter에서 data type이 먼저 나오는 Java와는 달리, kotlin에서는 data type이 뒤에 나온다. 그리고 제일 마지막에 return type이 나온다.

※ return type을 생략할 수 있는데, 함수 몸체가 식(Expression)인 경우 return 생략 가능하다.

즉 위와 같은 sum func의 경우에는 return이 생략 가능하다. ※

```
fum sum(a:Int, b:Int) = a+b  // return type이 '추론'된다.
```

2. Unit

Java의 void와 같다.

Unit은 하나의 single object이다.

```
fun printKotlin(): Unit{
    print("hello Kotlin")
}
```

※ Unit은 생략 가능하다 (아무것도 적지 않으면 Unit이 return된다 (void와 마찬가지로) )

3. 지역 변수

3-1) var : Mutable 변수 : Js의 var과 비슷하다고 보면 된다.

```
var x= 5;
```

3-2) val : 읽기 전용 변수

Java의 final과 유사하다.

```
val a: Int = 1;
var b = 2; /// data type 생략가능. data type을 '추론'한다.
```

4. 문자열 템플릿
###### String Interpolation (문자열 보간법)

```
var a= 1;
var s1 = "a is $a"

a=2;
val s2 = "${s1.replace("is","was")},but now is $a"
```
```
output : a was 1,but now is 2
```

5. 조건문

조건문은 자바와 비슷하다

```
fun maxOf(a:Int, b:Int):Int{
    if(a>b){
        return a;
    }else{
        return b;
    }
}
```
※ 조건식으로 축약해서 사용 가능 ※

```
fun maxOf(a:Int, b:Int) if(a>b) a else b
```

6. nullable

값이 null일 수 있는 경우, 타입에 null을 명시해주어야 한다.
null check를 안했는데, null이 리턴된다면 오류 발생.

```
fun parseInt(str: String): int?{
    ...
}
```

변수가 nullable일 경우에, 항상 null check를 하고 사용해야 한다.
(kotlin에서는 type이 안전하다고 불리는 이유다)

ex)

```
fun nullableTest(a1: String, a2: String){
    val x: Int? = parseInt(a1)
    val y: Int? = parseInt(a2)

    if(x!=null && y!=null){
        print(x*y)
    }
}
```

7. Any

java의 Object class개념.

```
fun getStringLength(obj:Any):Int?{
    if(obj is String){
        return obj.length
    }
    return null
}
```

8. while loop

java와 동일하다

9. when expression

java switch case. 그렇지만 java의 switch case 보다 더 강력하다.
( case에 int 뿐만 아니라 String, boolean등 여러 타입이 올 수 있다 )

```
fun describe(obj:Any):String={
    when(obj){
        1->"one"
        "Hello"->"Hi"
        is Long->"Long"
        !is Long->"Not a String"
        else ->"Unknown"
    }
}
```

10. ranges

In 연산자를 이용해서 숫자 범위 체크 가능

```
val x= 3
if(x in 1..10){
    print("fit in")
}
```

```
for(x in 1..5){
    print(x)
}
```

- 컬렉션도 in으로 loop가 가능하다.

```
val items = listOf("apple","banna","kiwi")
for(item in items){
    print(item)
}
```

- in으로 해당값이 collection에 포함되는지 체크 가능하다.

```
val items = setOf("apple","banna","kiwi")
when{
    "orange" in items -> println("juicy")
}
```

11. Collections

람다식을 이용해서 filter,map등의 연산이 가능하다
it = ->

```
val fruits = listOf("banana","avocado","apple","kiwi")

fruits.filter{it.startsWith("a")}
      .sortedBy{it}
      .map{it.toUpperCase()}
      .forEach{println(it)}
```
output : 
APPLE
AVOCADO