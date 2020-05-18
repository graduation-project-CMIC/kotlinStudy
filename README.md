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
output : a was 1,but now is 2
